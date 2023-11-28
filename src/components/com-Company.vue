<template>
  <main id="main">
    <div class="headerBG"></div>
    <section id="wines" class="wines">
      <div class="wines-left">
        <div class="wines-wrap">
          <div class="wines-list">
            <ul class="item-list">
              <!-- 태그가 달라질텐데 반복문 쓰면 안될듯... -->
              <li v-for="(x,i) in data" :key="i">
                {{ x.a}} : {{ x.b }}
              </li>
            </ul>
          </div>
        </div>
        <div class="info">
          <span class="btn-line infoBtn">PRODUCER INFO</span>
        </div>
      </div>
      <div class="wines-right">
        <div class="wines-imgBox">
          <img src="" alt="wines">
        </div>
      </div>
    </section>
    <section class="company" id="company">
      <div class="company-left">
        <div class="company-text">
          <h2>{{ data[2].b }}</h2>
          <h4>{{ data[3].b }}</h4>
          <p class="story-1">
            {{ data[7].b }}
          </p>
        </div>
        <span class="btn-line readBtn">READ MORE</span>
      </div>
      <div class="company-right">
        <div class="company-imgBox">
          <img src="" alt="company">
        </div>
      </div>
    </section>
    <div class="btn">
      <a class="btn-line" href="#">PREV</a>
      <span class="btn-line topBtn">TOP</span>
      <a class="btn-line" href="#">NEXT</a>
    </div>
  </main>
</template>

<script>
export default {
  data(){
    return{
      list : null,
      // 섹션1 사용할 데이터 담을거
      data : null,
      // 라우터 주소 /:id 받아온거
      routeParmasId : this.$route.params.id,
      a : null
    } 
  },
  components:{},
  props:['DataWineList'],
  methods : {
    // 공백제거 메소드
    textTrim(x){
      // 정규식을 이용한 공백제거 
      let text = x.replace(/(\s*)/g, "")
      // / 가 있는지 체크 
      if(text.split('/').length - 1 >= 1){
        // 있으면 / 를 다 지움
        text = text.replaceAll('/')
        return text;
      } else {
        // 없으면 공백만 제거해서 리턴
        return text;
      }
    }
  },
  created() {
    // 3중포문.

    // 빈 배열 만들어줌
    let a = [];
    let b = [];
    // 배열 한번 벗김
    this.DataWineList.forEach((ele)=>{
      a.push(...ele.data)
    })
    // 아마 객체인가 그래서 배열화 시킴
    for(let x of a){
      b.push(...x.LIST)
    }
    this.list = b


    // 누른놈이랑 같은이름 있으면 그놈 데이터 가져옴
    b.forEach((ele)=>{
      // 비교
      if(this.textTrim(ele.WINE) == this.routeParmasId){
        // 객체데이터여서 빈 배열 만들어서 data()에 있는 애한테 담기위해 만듬
        let arr = []
        // 이름 : 값 으로 배열화 
        for(let x in ele){
          let data = { a : x, b : ele[x]}
          arr.push(data)
        }
        // 템플릿에서 사용할 데이터에 담음
        this.data = arr
      }
    })


    let qqq=[];
    // console.log(this.DataWineList.length)
    // let qwer;
    for(let i = 0; i< this.DataWineList.length;i++){
      this.a = this.DataWineList[i].data.length;
      console.log(this.a)

      qqq.push(this.a);
    }
    console.log(qqq)
  },
}
</script>

<style scoped>
#main{
  position: relative;
}
.wines{
  width: 100%;
  height: 100vh;
  display: flex;
}

.wines-left,
.wines-right,
.company-left,
.company-right{
  width: 50%;
}

.wines-left{
  position: relative;
  margin-top: 59px;
}

.wines-wrap{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
}

.wines-list{
  overflow-y: auto;
  max-height: 360px;
}

.wines-wrap::before{
  content: '';
  position: absolute;
  bottom: 0%;
  background: linear-gradient(rgba(255, 255, 255, 0),var(--main));;
  width: 100%;
  height: 20%;
  pointer-events: none;
  z-index: 1;
}

.item-list{
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
}

.item{
  padding-bottom: 10px;
  transition: all .5s;
  cursor: pointer;
}

.item.colorB{
  color: var(--block);
}

.item.colorGray{
  color: rgba(0, 0, 0, 0.5);
}

.item:hover span{
  opacity: 1;
  transform: translateY(0%);
}

.item h3,
.item h4{
  font-size: var(--font-size-M);
  font-family: 'Nanum Myeongjo', serif;
  margin: 10px;
}

.item h4,
.company-text h4{
  font-style: italic;
}

.item span{
  font-size: var(--font-size-S);
  transform: translateY(50%);
  display: inline-block;
  opacity: 0;
  transition: all .5s;
}

.info{
  position: absolute;
  bottom: 10vh;
  left: 50%;
  transform: translateX(-50%);
}

.info a{
  font-size: var(--font-size-M);
}

.wines-right{
  background-color: var(--gray);
  padding-top: 59px;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: center;
}

.wines-imgBox{
  width: 55%;
  height: 80%;
  background-size: cover;
  background-position: center;
  transition: all .4s;
}

.company-left{
  background-color: var(--beige);
}

.company{
  display: flex;
}

.btn{
  position: absolute;
  bottom: 0;
  box-sizing: border-box;
  padding: 0 20px 20px;
  display: flex;
  justify-content: space-between;
  width: 100%;
  z-index: 2;
}

.btn a,
.btn span{
  font-size: var(--font-size-M);
}

.company-left{
  box-sizing: border-box;
  padding: 65px 100px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.company-text .story-2,
.company-text .story-3{
  transition: all 1s;
  height: 0;
  opacity: 0;
  visibility: hidden;
  overflow: hidden;
}

.story-2.active,
.story-3.active{
  overflow: auto;
  visibility: visible;
  opacity: 1;
}

.company-text h2,
.company-text h4,
.company-text p{
  text-align: center;
  font-size: var(--font-size-M);
  font-family: 'Nanum Myeongjo', serif;
  line-height: 1.3;
}

.company-text p{
  margin-top: 10px;
}

.readBtn{
  margin-top: 10px;
  cursor: pointer;
}

.company-right{
  height: 100vh;
  position: sticky;
  top: 0;
  background-color: var(--main);
  z-index: 2;
}

.company-imgBox{
  display: flex;
  width: 100%;
  height: 100%;
  align-items: center;
  justify-content: center;
}

.company-imgBox>img{
  object-fit: contain;
  width: 55%;
}

/* 미디어쿼리 */
@media screen and (max-width:990px){

  .wines-left{
    width: 100%;
  }

  .wines-right{
    display: none;
  }

  .company {
    width: 100%;
    display: flex;
    flex-direction: column-reverse;
    align-items: center;
  }

  .company-left,
  .company-right{
    width: 100%;
    height: 100%;
    background-color: var(--beige);
  }

  .company-right{
    position: static;
    padding-top: 65px;
    z-index: 0;
  }
}

/* 미디어쿼리 */
@media screen and (max-width:780px){

}
</style>