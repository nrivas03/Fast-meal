<template>
    <section style="background-color: #e6ccff;">
      <div class="mt-5">
        <h1>Comments</h1>
        <form >
            <input id="Name" type="text" v-model="name" >
            <input id="Comment" type="text" v-model="comment" >
            <button @click="addComment">Submit</button>
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
              <div>
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
     addComment: function(){
      let date = new Date();
      let day = date.toUTCString()
      this.comments.push({
        name: this.name,
        comment: this.comment,
        date: day,
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

