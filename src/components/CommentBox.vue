<template>
    <section style="background-color: #e6ccff;">
      <div class="mt-5">
        <h1>Comments</h1>
        <form >
            <input id="Name" type="text" v-model="name" placeholder="User name" maxlength="25">
            <input class="comment" id="Comment" type="text" v-model="comment" placeholder="Comment" maxlength="500">
            <button class="buttonsubmit" @click="addComment($route.params.id)">Submit</button>
        </form>
    </div>
  <div class="container my-5 py-5">    
    <div class="row d-flex justify-content-center">     
      <div class="col-md-12 col-lg-10">
        <div class="card text-dark">         
          <div class="card-body p-4">
            <h4 class="mb-0">Recent comments</h4>
            <p class="fw-light mb-4 pb-2">Latest Comments section by users</p>
            <div class="d-flex flex-start" v-for="item of comments">
              <div v-if="item.idMeal==$route.params.id">
                <h6 class="fw-bold mb-1">{{item.name}}</h6>
                <div class="d-flex align-items-center mb-3">
                  <p class="mb-0">
                    {{item.date}}
                  </p>
                  <a href="#!" class="link-muted"><i class="fas fa-pencil-alt ms-2"></i></a>
                  <a href="#!" class="link-muted"><i class="fas fa-redo-alt ms-2"></i></a>
                  <a href="#!" class="link-muted"><i class="fas fa-heart ms-2"></i></a>
                </div>
                <p class="mb-0">
                  {{item.comment}}
                </p>
              </div>
            </div>

          </div>
          
          <hr class="my-0" />
        </div>
      </div>
    </div>
  </div>
</section>

</template>



<style scoped>
    .link-muted { color: #aaa; } .link-muted:hover { color: #1266f1; }
    
    .buttonsubmit{
      background-color: #c53fd4; color: rgb(255, 255, 255);
      padding: 9px 25px;
      box-shadow: 0 8px 13px 0 rgba(0, 0, 0, 0.68), 0 6px 20px 0 rgba(0,0,0,0.19);
      position: relative;
      left: 15px;
    }

    .comment{
      position: relative;
      left: 5px;
    }
</style>

<script>
  export default{
  data(){
    return{
      name: '',
      comment:'',
      comments:[],
    }
  },
  mounted() {
    this.getComments();
  },
  methods:{
     addComment: function(route){
      let date = new Date();
      let day = date.toUTCString()
      this.comments.push({
        name: this.name,
        comment: this.comment,
        date: day,
        idMeal: route,
      });
      console.log(this.comments);
      localStorage.setItem("comments", JSON.stringify(this.comments));
    },
    async getComments(){
      let data = localStorage.getItem("comments");
      if(data !=null){
        this.comments = JSON.parse(data);
      }
    },

  }
};
</script>

