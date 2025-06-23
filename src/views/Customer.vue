<template>
  <div class="customer-page">
    <form class="search-bar" @submit.prevent="doSearch">
      <el-input v-model="searchName" :placeholder="$t('customer.search.name')" style="width: 160px" clearable />
      <el-input v-model="searchEmail" :placeholder="$t('customer.search.email')" style="width: 180px" clearable />
      <el-date-picker
        v-model="searchDate"
        type="date"
        :placeholder="$t('customer.search.date')"
        value-format="yyyy-MM-dd"
        style="width: 160px"
      />
      <button type="submit" class="search-btn">{{ $t('customer.search.searchBtn') }}</button>
      <button type="button" class="reset-btn" @click="resetSearch">{{ $t('customer.search.resetBtn') }}</button>
    </form>
    <div>
      <h2>{{ $t('customer.title') }}</h2> 
      <div class="table-wrapper">
        <table class="customer-table">
          <thead>
            <tr>
              <th>{{ $t('customer.table.name') }}</th>
              <th>{{ $t('customer.table.email') }}</th>
              <th>{{ $t('customer.table.tittle') }}</th>
              <th :class="'message-col'">{{ $t('customer.table.message') }}</th>
              <th>{{ $t('customer.table.time') }}</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, idx) in customers" :key="idx">
              <td>{{ item.name }}</td>
              <td>{{ item.email }}</td>
              <td>{{ item.tittle }}</td>
              <td :class="'message-col'">{{ item.message }}</td>
              <td>{{ formatTime(item.time) }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <el-pagination
        v-if="total > size"
        :current-page="page"
        :page-size="size"
        :total="total"
        :page-sizes="[5, 10, 20, 50]"
        layout="total, sizes, prev, pager, next, jumper"
        @current-change="handlePageChange"
        @size-change="handleSizeChange"
        background
        style="margin: 20px 0; text-align: right;"
      />
    </div>
  </div>
</template>

<script>
import { DatePicker, Input, Pagination } from 'element-ui'
function formatTime(val) {
  if (!val) return ''
  // 兼容 "2024-05-01T12:00:00" 或 "2024-05-01 12:00:00"
  let d = val.replace('T', ' ')
  if (d.length > 19) d = d.slice(0, 19)
  return d
}
export default {
  name: 'Customer',
  components: {
    'el-date-picker': DatePicker,
    'el-input': Input,
    'el-pagination': Pagination
  },
  data() {
    return {
      customers: [],
      showList: false,
      searchDate: '',
      searchName: '',
      searchEmail: '',
      page: 1,
      size: 10,
      total: 0,
      loading: false
    }
  },
  mounted() {
    if (localStorage.getItem('customer_authed') === '1') {
      this.showList = true;
      this.fetchCustomers();
    } else {
      this.askPassword();
    }
  },
  methods: {
    askPassword() {
      const pwd = prompt('请输入管理员口令：');
      if (pwd === 'kl2025') {
        this.showList = true;
        this.fetchCustomers();
      } else {
        alert('口令错误！');
        this.$router.replace('/')
      }
    },
    async fetchCustomers() {
      this.loading = true;
      try {
        const params = {
          name: this.searchName,
          email: this.searchEmail,
          time: this.searchDate,
          page: this.page,
          size: this.size
        }
        Object.keys(params).forEach(key => {
          if (!params[key]) delete params[key]
        })
        const res = await this.$axios.get('http://localhost:8080/api/user-contacts/list', { params })
        this.customers = res.data.list || res.data.data || []
        this.total = res.data.total || 0
      } catch (e) {
        alert('查询失败')
      }
      this.loading = false;
    },
    doSearch() {
      this.page = 1;
      this.fetchCustomers();
    },
    resetSearch() {
      this.searchName = '';
      this.searchEmail = '';
      this.searchDate = '';
      this.page = 1;
      this.fetchCustomers();
    },
    handlePageChange(val) {
      this.page = val;
      this.fetchCustomers();
    },
    handleSizeChange(val) {
      this.size = val;
      this.page = 1;
      this.fetchCustomers();
    },
    formatTime
  },
  beforeRouteLeave(to, from, next) {
    localStorage.removeItem('customer_authed');
    next();
  }
}
</script>

<style scoped>
.customer-page {
  max-width: 900px;
  margin: 40px auto;
  padding: 24px;
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 8px 32px rgba(80,80,160,0.08);
}
.search-bar {
  display: flex;
  gap: 18px;
  margin-bottom: 18px;
  align-items: center;
  flex-wrap: wrap;
}
.search-bar input {
  padding: 8px 12px;
  border: 1.5px solid #e1e5ea;
  border-radius: 8px;
  font-size: 1rem;
  min-width: 120px;
}
.search-btn, .reset-btn {
  padding: 8px 18px;
  border-radius: 8px;
  border: none;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  margin-left: 2px;
  transition: background 0.2s;
}
.search-btn {
  background: #667eea;
  color: #fff;
}
.search-btn:hover {
  background: #764ba2;
}
.reset-btn {
  background: #f7f8fa;
  color: #333;
  border: 1.5px solid #e1e5ea;
}
.reset-btn:hover {
  background: #e1e5ea;
}
.customer-page h2 {
  color: #667eea;
  font-weight: 700;
  margin-bottom: 24px;
}
.table-wrapper {
  width: 100%;
  /* 电脑端不设置overflow-x，表格自然撑满 */
}
.customer-table {
  width: 100%;
  border-collapse: collapse;
  background: #f7f8fa;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(80,80,160,0.04);
}
.customer-table th, .customer-table td {
  padding: 14px 10px;
  border-bottom: 1px solid #e1e5ea;
  text-align: left;
  font-size: 1rem;
}
.customer-table th.message-col, .customer-table td.message-col {
  width: 40%;
  min-width: 320px;
  word-break: break-all;
}
.customer-table th {
  background: #667eea;
  color: #fff;
  font-weight: 600;
}
.customer-table tr:last-child td {
  border-bottom: none;
}
@media (max-width: 900px) {
  .table-wrapper {
    overflow-x: auto;
  }
  .customer-table {
    min-width: 700px;
  }
  .el-pagination {
    width: 100%;
    justify-content: center;
    display: flex !important;
    flex-wrap: wrap;
  }
}
@media (max-width: 600px) {
  .customer-page {
    padding: 8px;
    margin: 10px auto;
  }
  .search-bar {
    flex-direction: column;
    gap: 10px;
    align-items: stretch;
  }
  .search-bar input,
  .search-btn,
  .reset-btn {
    width: 100%;
    min-width: 0;
    box-sizing: border-box;
    margin-left: 0;
  }
  .customer-page h2 {
    font-size: 1.1rem;
    margin-bottom: 12px;
  }
  .table-wrapper {
    margin-bottom: 10px;
  }
  .customer-table th, .customer-table td {
    font-size: 0.92rem;
    padding: 7px 4px;
  }
  .el-pagination {
    width: 100%;
    justify-content: center;
    display: flex !important;
    flex-wrap: wrap;
  }
}
</style> 