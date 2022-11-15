<template>
  <div v-if="currentUser" class="text-center">
    <div style="margin-bottom: 60px"></div>
    <img :src="require('../assets/user.png')" alt="logo" />
    <div><h1>Bonjour {{ currentUser.username }}</h1></div>
  </div>
  <div v-else >
    <div style="background-image: url('1440_650.png'); padding-top:60px; padding-bottom: 60px; background-size:100%">
        <h2 class="text-center">Lorem Ipsum</h2>
        <p style = "font-size:23px" class="text-center">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque pellentesque.</p>
        <p style = "font-size:20px" class="text-center">
          "Neque porro quisquam est qui dolorem ipsum <br>
          quia dolor sit amet, consectetur, adipisci <br>
          velit..."
        </p>
        <div style="margin-bottom: 40px"></div>
        <div class="input-group mb-3 justify-content-center">
          <input type="text" class="form-control" style="height: 70px; flex: none; width: 400px; border-radius: 10px 0 0 10px; border-color:rgb(150,150,150)" placeholder="Adresse e-mail" aria-label="Adresse e-mail" aria-describedby="button-addon2">
          <div class="input-group-append">
            <button class="btn btn-outline-secondary" style="height: 70px; background-color: rgb(47, 205, 255); border-radius: 0 10px 10px 0; border-color:rgb(150,150,150); color: white;" type="button" id="button-addon2">Commencer ></button>
          </div>
        </div>
    </div>

    <div style="height:10px; background-color: rgb(50, 50, 50); margin-bottom: 60px">
    </div>
    <div class="container" style = "width:900px">
       <div class= "row">
          <div class="col-6" >
            <h3 >Lorem ipsum dolor sit amet.</h3>
            <p style ="font-size:20px"> In posuere malesuada ex sit amet sagittis. <br>
                Mauris aliquam dui nec nisl convallis <br>
                lobortis.Lorem ipsum dolor sit amet, <br>
                consectetur adipiscing elit <br>
            </p>
          </div>
                
          <div class="col-6">
            <img :src="require('../assets/400_200.png')" />
          </div>
      </div>
    </div>
    
    <div style="margin-bottom: 60px"></div>
    
    <div style="height:10px; background-color: rgb(50, 50, 50); margin-bottom: 60px">
    </div>

    <div class="container" style = "width:900px">
       <div class= "row">
         
                
          <div class="col-6">
            <img :src="require('../assets/400_200.png')" />
          </div>
          <div class="col-6" >
            <h3 >Lorem ipsum dolor sit amet.</h3>
            <p style ="font-size:20px"> In posuere malesuada ex sit amet sagittis. <br>
                Mauris aliquam dui nec nisl convallis <br>
                lobortis.Lorem ipsum dolor sit amet, <br>
                consectetur adipiscing elit <br>
            </p>
          </div>
      </div>
    </div>

    <div style="margin-bottom: 60px"></div>

    <div style="height:10px; background-color: rgb(50, 50, 50); margin-bottom: 60px">
    </div>

    <div class="container" style = "width:900px">
       <div class= "row">
          <div class="col-6" >
            <h3 >Lorem ipsum dolor sit amet.</h3>
            <p style ="font-size:20px"> In posuere malesuada ex sit amet sagittis. <br>
                Mauris aliquam dui nec nisl convallis <br>
                lobortis.Lorem ipsum dolor sit amet, <br>
                consectetur adipiscing elit <br>
            </p>
          </div>
                
          <div class="col-6">
            <img :src="require('../assets/400_200.png')" />
          </div>
      </div>
    </div>

    <div style="margin-bottom: 60px"></div>
   
    <div style="height:10px; background-color: rgb(50, 50, 50); margin-bottom: 60px">
    </div>
    <div class="container">
      <h3 >Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur at tincidunt tellus.</h3>
      
      <div style="margin-bottom: 60px"></div>

      <div class="input-group mb-3 justify-content-center">
        <input type="text" class="form-control" style="height: 70px; flex: none; width: 400px; border-radius: 10px 0 0 10px; border-color:rgb(150,150,150)" placeholder="Adresse e-mail" aria-label="Adresse e-mail" aria-describedby="button-addon2">
        <div class="input-group-append">
          <button class="btn btn-outline-secondary" style="height: 70px; background-color: rgb(47, 205, 255); border-radius: 0 10px 10px 0; border-color:rgb(150,150,150); color: white;" type="button" id="button-addon2">Commencer ></button>
        </div>
      </div>
    </div>
    <div style="margin-bottom: 60px"></div>

  </div>
 
    
</template>

<script>
import UserService from "../services/user.service";

export default {
  name: "Home",
  computed: {
    currentUser() {
      return this.$store.state.auth.user;
    },
  },
  data() {
    return {
      content: "",
    };
  },
  mounted() {
    UserService.getPublicContent().then(
      (response) => {
        this.content = response.data;
      },
      (error) => {
        this.content =
          (error.response &&
            error.response.data &&
            error.response.data.message) ||
          error.message ||
          error.toString();
      }
    );
  },
};
</script>
