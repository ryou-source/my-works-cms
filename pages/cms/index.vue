<template>
  <el-container>
    <el-header>
      <el-row>
        <el-col :span="24">
          <h1>My-Works-CMS</h1>
        </el-col>
      </el-row>
    </el-header>
    <el-main>
      <el-table
        :data="works"
        style="width: 100%">
        <el-table-column
          label="Date">
          <template slot-scope="scope">
            <i class="el-icon-time"></i>
            <span style="margin-left: 10px">{{ scope.row.created.toDate() | dateFilter }}</span>
          </template>
        </el-table-column>
        <el-table-column
          label="Title">
          <template slot-scope="scope">
            <div slot="reference" class="name-wrapper">
              <span>{{ scope.row.title }}</span>
            </div>
          </template>
        </el-table-column>
        <el-table-column
          label="Operations">
          <template slot-scope="scope">
            <el-button
              size="mini"
              @click="handleEdit(scope.row)">編集</el-button>
            <el-button
              size="mini"
              type="danger"
              @click="remove(scope.row.id)">削除</el-button>
          </template>
        </el-table-column>
      </el-table>
    </el-main>
  </el-container>
</template>


<script>
import moment from "moment"
export default {
  created() {
    this.$store.dispatch("works/init")
  },
  computed:{
    works(){
      return this.$store.getters['works/orderdWorks']
    }
  },
  methods:{
    remove(id){
      this.$store.dispatch("works/remove",id)
    },
    handleEdit(row) {
      this.$store.dispatch("works/edit",row)
    },
  },
  filters:{
    dateFilter(date){
      return moment(date).format("YYYY/MM/DD HH:mm:ss")
    }
  }
}
</script>

<style lang="scss" scoped>
.el-header{
  .el-row{
    .el-col.el-col-24{
      display: flex;
      justify-content: center;
      align-items: center;
    }
  }
}
/deep/.el-main{
  padding: 0;
  .el-table.el-table--fit.el-table--enable-row-hover{
    .el-table__header-wrapper{
      .el-table__header{
        .has-gutter{
          >tr{
            >th{
              text-align: center;
            }
          }
        }
      }
    }
    .el-table__row{
      >td{
        text-align: center;
      }
    }
  }
}
</style>