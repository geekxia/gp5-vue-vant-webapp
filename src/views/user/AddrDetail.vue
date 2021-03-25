<template>
<div class="qf-addr-detail">

  <QfNavbar title="地址新增" />
  <van-address-edit
    :area-list="areaList"
    show-postal
    show-set-default
    show-search-result
    :search-result="searchResult"
    :area-columns-placeholder="['请选择', '请选择', '请选择']"
    @save="onSave"
  />
</div>
</template>

<script>
import { QfNavbar } from '@/components'
export default {
  components: {
    QfNavbar
  },
  data() {
    return {
      areaList:{
        province_list: {
          110000: '北京市',
          120000: '天津市'
        },
        city_list: {
          110100: '北京市',
          110200: '县',
          120100: '天津市',
          120200: '县'
        },
        county_list: {
          110101: '东城区',
          110102: '西城区',
          110105: '朝阳区',
          110106: '丰台区',
          120101: '和平区',
          120102: '河东区',
          120103: '河西区',
          120104: '南开区',
          120105: '河北区'
        }
      },
      searchResult: []
    }
  },
  methods: {
    onSave(e) {
      console.log('save', e)
      const data = {
        receiver: e.name,
        mobile: e.tel,
        addr: `${e.province}${e.city}${e.county}`,
        primary: e.isDefault
      }
      this.$api.fetchAddrAdd(data).then(()=>{
        this.$router.back()
      })
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
