<template>
       <div class="swiper_wraper">
            <div class="weiper_inner w960">
                     <div class="lunbo">
                              <el-carousel height="260px">
                                    <el-carousel-item v-for="(item,index) in bannerlist" :key="index">
                                        <img :src="item.imgurl" alt="">
                                    </el-carousel-item>
                             </el-carousel>
                     </div>
                     <div class="blog_boss">
                           <el-card class="mycard">
                                  <h2>我的卡片</h2>
                                  <p><span>网名：</span><span>慕圣</span></p>
                                  <p><span>职业：</span><span>web前端工程师</span></p>
                                  <p><span>phone：</span><span>null</span></p>
                                  <p><span>email：</span><span>xundw@qq.com</span></p>
                                  <div class="personmessae">
                                        <ul>
                                            <li class="per_item"></li>
                                            <li class="per_item"></li>
                                            <li class="per_item"></li>
                                            <li class="per_item"></li>
                                     
                                        </ul>
                                  </div>
                           </el-card>
                     </div>
            </div>
            <div class="body_inner w960">
                   <el-row>
                       <el-col :span="18" class="article_wrepr">
                               <special></special>
                               <newarticle></newarticle>
                       </el-col>
                       <el-col :span="6" class="newblog_list">
                            <div class='title_waraper'>
                                  最新发布
                            </div>
                            <ul>
                                <li class="blog_list_item" v-for="(blog,index) in blogList" :key="index">
                                     <p>
                                      {{blog.title}}
                                    </p>  
                                </li>
                            </ul>
                            <div class="blog_author">
                                 <blog-author>
                                     
                                 </blog-author>
                            </div>
                       </el-col>
                   </el-row>
            </div>
      </div>
</template>
<script>
import special from '../../components/Newest'
import newarticle from '../../components/Newarticle'
import blogAuthor from '../../components/Blogperson'
    export default
    {
           name:'homeindex',
               data(){
            return{
              bannerlist:[],
              blogList:[]
            }
        },
        components:{
               special,
               newarticle,
               blogAuthor
        },
        methods:{
            getbanner(){
                this.$axios.get('/banner').then(res=>{
                    this.bannerlist =res.data
                })
            },
            async getNewBlog(){
               let data =await this.$axios.get('/blog/new')
               console.log(data)
               if(data.code == 200){
                   this.blogList = data.data
               }
            }
        },
        created(){
            this.getbanner()
            this.getNewBlog()
        }

    }
</script>

<style scoped lang ='scss'>
.body_inner{
    margin: 0 auto;
    .article_wrepr{
        margin-top: 30px;
     
    }
}
.swiper_wraper{
    padding: 30px;
    .weiper_inner{
        margin: 0 auto;
        display: flex;
        justify-content: space-between;
    }  
}
.lunbo{
    width: 700px;
    border-radius: 6px;
    overflow: hidden;
}
.blog_boss{
    width: 250px;
    .mycard{
        height: 260px;;
        background-color: #2A2A2A;
        border: none;
        h2{
            font-size: 19px;
            color: #3F3E3C;
        }
        p{
            line-height: 35px;
            margin-top: 8px;
            font: 13px "宋体", "Arial Narrow", HELVETICA;
            color: #89919A;
        }
    }
}
.personmessae{
       margin-top: 40px;
    ul{
        display: flex;
        justify-content: space-around;
    }
    .per_item{
        height: 45px;
        width: 45px;
        border-radius: 50%;
        box-shadow: 1px 2px 4px rgba(0,0,0,.2),inset 0 1px 1px rgba(0,0,0,.7);
        background-color: #3F3E3C;
    }
}
.newblog_list{
     margin-top: 30px;
     background-color: #2A2A2A;
     border-radius: 10px;
     font-family: '宋体';
     padding: 20px;
     box-sizing: border-box;

}
.title_waraper{
    text-align: center;
    border-bottom: 2px dashed #333;
    color: #ddd;
    padding-bottom: 10px;

}
.blog_list_item{
    margin-top: 10px;
    p{
        cursor: pointer;
        height: 30px;
        line-height: 30px;
        font: 14px '宋体';
        transition: all .2s linear;
        color: #ddd;
    }
    p:hover{
        font-size: 15px;
        color: #ff0;
    }
}
</style>
