<template>
  <view class="home-page content">
    <view class="search">
      <u-search v-model="keyword" shape="round" placeholder="搜索医生/病友/日记/问答/话题" :show-action="false"></u-search>
    </view>
    <!-- <u-tabs :list="list" :is-scroll="false" :current="current" @change="change"></u-tabs> -->
    <!-- <rich-text :nodes="strings"></rich-text> -->
    <view class="wrap">
      <u-button @click="clear">清空列表</u-button>
      <u-waterfall ref="uWaterfall" v-model="flowList">
        <template v-slot:left="{leftList}">
          <view v-for="(item, index) in leftList" :key="index" class="demo-warter">
            <!-- 警告：微信小程序中需要hx2.8.11版本才支持在template中结合其他组件，比如下方的lazy-load组件 -->
            <u-lazy-load threshold="-450" border-radius="10" :image="item.image" :index="index"></u-lazy-load>
            <view class="demo-title">
              {{ item.title }}
            </view>
            <view class="demo-price">
              {{ item.price }}元
            </view>
            <view class="demo-tag">
              <view class="demo-tag-owner">
                自营
              </view>
              <view class="demo-tag-text">
                放心购
              </view>
            </view>
            <view class="demo-shop">
              {{ item.shop }}
            </view>
            <u-icon name="close-circle-fill" color="#fa3534" size="34" class="u-close" @click="remove(item.id)"></u-icon>
          </view>
        </template>
        <template v-slot:right="{rightList}">
          <view v-for="(item, index) in rightList" :key="index" class="demo-warter">
            <u-lazy-load threshold="-450" border-radius="10" :image="item.image" :index="index"></u-lazy-load>
            <view class="demo-title">
              {{ item.title }}
            </view>
            <view class="demo-price">
              {{ item.price }}元
            </view>
            <view class="demo-tag">
              <view class="demo-tag-owner">
                自营
              </view>
              <view class="demo-tag-text">
                放心购
              </view>
            </view>
            <view class="demo-shop">
              {{ item.shop }}
            </view>
            <u-icon name="close-circle-fill" color="#fa3534" size="34" class="u-close" @click="remove(item.id)"></u-icon>
          </view>
        </template>
      </u-waterfall>
      <u-loadmore bg-color="rgb(240, 240, 240)" :status="loadStatus" @loadmore="addRandomData"></u-loadmore>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      keyword: '',
      // list: [{
      //   name: '待收货'
      // }, {
      //   name: '待付款'
      // }, {
      //   name: '待评价'
      // }],
      current: 0,
      strings: '',
      loadStatus: 'loadmore',
      flowList: [],
      list: [
        {
          price: 35,
          title: '北国风光，千里冰封，万里雪飘',
          shop: '李白杜甫白居易旗舰店',
          image: 'https://equah-frontend-test.oss-cn-hangzhou.aliyuncs.com/equah-mini/images/fack_banner.jpg'
        },
        {
          price: 75,
          title: '望长城内外，惟余莽莽',
          shop: '李白杜甫白居易旗舰店',
          image: 'https://equah-frontend-test.oss-cn-hangzhou.aliyuncs.com/equah-mini/images/index_banner_01.png'
        }
      ]
    }
  },
  onLoad() {
    // const nodes = '<div class="article-content"><h1>中国每天有一万人确诊癌症？50岁以后，晚上坚持“2多4少”</h1><div class="article-meta"><span>2021-06-08 10:34</span><span class="dot">·</span><span class="name"><a href="/c/user/token/MS4wLjABAAAAnZReDAvDgfZyN8NAAMH-hAuGrcrKew1JH7rusau08wc/?source=tuwen_detail" target="_blank" rel="noopener">家庭医生名医在线</a></span></div><article class="syl-article-base syl-page-article syl-device-pc tt-article-content"><p style="text-align: left;text-indent: 2em;" data-track="1"><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">人人都怕癌，但癌症的发病率却逐年升高，给患者和家庭带来沉重的负担。癌症是多种因素共同的结果，如遗传和环境以及生活习惯等。特别是中老年人，患癌症的风险最高，若想要远离癌症应调整好生活习惯，晚上坚持“2多4少”。</span></p><div class="pgc-img"><img src="https://p1-tt.byteimg.com/origin/pgc-image/1d955c2cbda04b6bb377a30ad24165c2?from=pc" img_width="1023" img_height="682" alt="中国每天有一万人确诊癌症？50岁以后，晚上坚持“2多4少”" inline="0" class="syl-page-img"><p class="pgc-img-caption"></p></div><h1 class="pgc-h-arrow-right" data-track="2">50岁以上的人怎么做才能远离癌症？</h1><p style="text-align: left;text-indent: 2em;" data-track="3"><strong><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">1、多运动</span></strong></p><p style="text-align: left;text-indent: 2em;" data-track="4"><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">晚饭后抽出30分钟的时间户外运动，如快步走、跳广场舞、慢跑以及打球等，能帮助消耗体内多余热量，加快胃肠道蠕动，促进食物消化。晚上运动也能提高基础代谢率，帮助稳定血压，调节血脂和降低血糖。但睡觉前半个小时内不能做剧烈运动，以免兴奋中枢神经，反而会影响睡眠。</span></p><p style="text-align: left;text-indent: 2em;" data-track="5"><strong><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">2、多饮食清淡</span></strong></p><p style="text-align: left;text-indent: 2em;" data-track="6"><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">晚餐质量和数量直接决定人们的健康程度，晚餐吃得太多或太油腻，不仅增加肠胃负担，易引起胃食管反流，而且也影响睡眠质量，增加患癌风险，特别是食管癌。所以晚餐以清淡、易消化为主，不妨选择新鲜蔬菜水果和各种粥类。另外，晚餐也不能吃得太饱，感觉6~7分饱就行。</span></p><p style="text-align: left;text-indent: 2em;" data-track="7"><strong><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">3、少熬夜</span></strong></p><p style="text-align: left;text-indent: 2em;" data-track="8"><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">虽然熬夜易成为现代人的家常便饭，不过这种行为不可取。人一生中1/3的时间在睡眠中度过，只有优质且充足睡眠才能让体力和精力恢复，促进细胞修复和再生，让全身各个器官得到足够血液滋养，从而提高抵抗力和免疫力，降低患癌风险。保证23点之前入睡，成年人每天睡够7个小时。</span></p><div class="pgc-img"><img src="https://p1-tt.byteimg.com/origin/pgc-image/872eebe82d0e4a46b15e2902c205b7df?from=pc" img_width="1200" img_height="914" alt="中国每天有一万人确诊癌症？50岁以后，晚上坚持“2多4少”" inline="0" class="syl-page-img"><p class="pgc-img-caption"></p></div><p style="text-align: left;text-indent: 2em;" data-track="9"><strong><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">4、少喝酒</span></strong></p><p style="text-align: left;text-indent: 2em;" data-track="10"><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">相当一部分人习惯睡前小酌一杯，认为能促眠和助兴，但这是非常危险的行为。睡前喝酒会使得睡眠质量更加糟糕，同时也会损害肝细胞和胃黏膜，若习惯睡觉前酗酒可增加患肝癌和胃癌以及胰腺癌风险。所以睡觉前拒绝喝酒，最安全的喝酒量应该是0，也就是滴酒不沾。</span></p><p style="text-align: left;text-indent: 2em;" data-track="11"><strong><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">5、少吃加工类食品</span></strong></p><p style="text-align: left;text-indent: 2em;" data-track="12"><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">晚上少吃或不吃加工食品，如各种糕点、腌制熏制和油炸食品等，这属于高油、高盐、高糖食物，不仅仅造成身体肥胖，而且也会增加肠胃负担，同时也提高患癌风险。</span></p><p style="text-align: left;text-indent: 2em;" data-track="13"><strong><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">6、少吸烟</span></strong></p><p style="text-align: left;text-indent: 2em;" data-track="14"><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">晚上基础代谢率降低，晚上吸太多烟对身体带来的危害会翻倍，香烟中的致癌物和有害物可直接侵害身体各个器官，增加患肺癌、胃癌以及血癌风险。因此晚上拒绝吸烟，尤其是睡觉前三个小时。</span></p><div class="pgc-img"><img src="https://p1-tt.byteimg.com/origin/pgc-image/98d7744e5963428bb7d8f9ecf391dc87?from=pc" img_width="800" img_height="533" alt="中国每天有一万人确诊癌症？50岁以后，晚上坚持“2多4少”" inline="0" class="syl-page-img"><p class="pgc-img-caption"></p></div><p style="text-align: left;text-indent: 2em;" data-track="15"><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">温馨提示</span></p><p style="text-align: left;text-indent: 2em;" data-track="16"><span style="color: #000000; --tt-darkmode-color: #A3A3A3;">癌症并不是无缘无故产生的，其生活因素占一大部分，所以应做好生活调理。及时改变不良的生活习惯如吸烟喝酒，少吃或不吃腌制熏制食物，注意饮食多样化，多运动来维持正常体重。远离高污染环境，生活中不能接触促癌剂和致癌剂，职业工作者应做好职业防护。平时应多留意自身症状，若出现顽固性消化不良、接触性阴道出血、溃疡持续不愈合以及排便习惯发生改变等，应及早去医院做防癌筛查。科学规范且及早治疗癌前病变，有癌症家族史的人应提前做防癌筛查。</span></p><p data-track="17"><strong>家庭医生在线专稿，未经授权不得转载</strong></p><p data-track="18"><a class="tteditor-forum" data-name="健康明星计划" data-uid="" data-id="1683780398823471" data-concern-id="1683780398823471" rel="noopener noreferrer">#健康明星计划#</a> </p></article></div>'
    // this.strings = nodes.replace(/\<img/gi, '<img style="max-width:100%;height:auto" ')
    this.addRandomData()
  },
  methods: {
    change(index) {
      this.current = index
    },
    addRandomData() {
      for (let i = 0; i < 10; i++) {
        const index = this.$u.random(0, this.list.length - 1)
        // 先转成字符串再转成对象，避免数组对象引用导致数据混乱
        const item = JSON.parse(JSON.stringify(this.list[index]))
        item.id = this.$u.guid()
        this.flowList.push(item)
      }
    },
    remove(id) {
      this.$refs.uWaterfall.remove(id)
    },
    clear() {
      this.$refs.uWaterfall.clear()
    }
  }
}
</script>

<style lang="scss">
.home-page{
	.search{
	width: 90%;
	margin: 50rpx auto;
	.u-search{
		.u-content{
			height: 40px !important;
			}
		}
	}
}
.demo-warter {
		border-radius: 8px;
		margin: 5px;
		background-color: #ffffff;
		padding: 8px;
		position: relative;
	}

	.u-close {
		position: absolute;
		top: 32rpx;
		right: 32rpx;
	}

	.demo-image {
		width: 100%;
		border-radius: 4px;
	}

	.demo-title {
		font-size: 30rpx;
		margin-top: 5px;
		color: $u-main-color;
	}

	.demo-tag {
		display: flex;
		margin-top: 5px;
	}

	.demo-tag-owner {
		background-color: $u-type-error;
		color: #FFFFFF;
		display: flex;
		align-items: center;
		padding: 4rpx 14rpx;
		border-radius: 50rpx;
		font-size: 20rpx;
		line-height: 1;
	}

	.demo-tag-text {
		border: 1px solid $u-type-primary;
		color: $u-type-primary;
		margin-left: 10px;
		border-radius: 50rpx;
		line-height: 1;
		padding: 4rpx 14rpx;
		display: flex;
		align-items: center;
		border-radius: 50rpx;
		font-size: 20rpx;
	}

	.demo-price {
		font-size: 30rpx;
		color: $u-type-error;
		margin-top: 5px;
	}

	.demo-shop {
		font-size: 22rpx;
		color: $u-tips-color;
		margin-top: 5px;
	}
</style>
