<template>
<div class='qf-addr'>

  <QfNavbar title="地址列表" />

  <van-address-list
    v-model="addrId"
    :list="list"
    default-tag-text="默认"
    @add="onAdd"
  />
</div>
</template>

<script>
import { QfNavbar } from '@/components'
export default {
  name: 'Addr',
  components: {
    QfNavbar
  },
  data() {
    return {
      addrId: '',
      list: []
    }
  },
  mounted() {
    this.init()
  },
  watch: {
    addrId() {
      const params = {
        addr_id: this.addrId
      }
      this.$api.fetchUpdDefAddr(params).then(()=>{
        this.init()
      })
    }
  },
  methods: {
    init() {
      this.$api.fetchAddrList({}).then(res=>{
        console.log('addr', res)
        this.list = this.listTranfer(res.list)
        this.addrId = res.list.find(ele=>ele.primary)._id
      })
    },
    listTranfer(list){
      return list.map(ele=>(
        {
          id: ele._id,
          name: ele.receiver,
          tel: ele.mobile,
          address: ele.addr,
          isDefault: ele.primary,
        }
      ))
    },
    onAdd() {
      console.log('add')
      this.$router.push('/user/addr/0')
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
