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
        
        <form ref="form" style= "display:none" @submit.prevent="sendEmail">
          <label>Name</label>
          <input type="text" name="to_name" v-model="to_name">
          <label>Email</label>
          <input type="text" name="from_name" v-model="from_name">
          
          <input type="email" name="to_email" v-model="sub_email">
          <label>Message</label>
          <textarea name="message" v-model="test_message"></textarea>
          <input type="submit" value="Send">
        </form>

        <div style="margin-bottom: 40px"></div>
        <div class="input-group mb-3 justify-content-center">
          <input v-model="sub_email" type="email" class="form-control" style="height: 70px; flex: none; width: 400px; border-radius: 10px 0 0 10px; border-color:rgb(150,150,150)" placeholder="Adresse e-mail" aria-label="Adresse e-mail" aria-describedby="button-addon2">
          <div class="input-group-append">
            <button @click="handleSubscribe" class="btn btn-outline-secondary" style="height: 70px; background-color: rgb(47, 205, 255); border-radius: 0 10px 10px 0; border-color:rgb(150,150,150); color: white;" type="button" id="button-addon2">Commencer ></button>
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
        <input v-model="sub_email" type="text" class="form-control" style="height: 70px; flex: none; width: 400px; border-radius: 10px 0 0 10px; border-color:rgb(150,150,150)" placeholder="Adresse e-mail" aria-label="Adresse e-mail" aria-describedby="button-addon2">
        <div class="input-group-append">
          <button @click="handleSubscribe" class="btn btn-outline-secondary" style="height: 70px; background-color: rgb(47, 205, 255); border-radius: 0 10px 10px 0; border-color:rgb(150,150,150); color: white;" type="button" id="button-addon2">Commencer ></button>
        </div>
      </div>
    </div>
    <div style="margin-bottom: 60px"></div>

  </div>
 
    
</template>
<script>
import UserService from "../services/user.service";
import emailjs from '@emailjs/browser';

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
      sub_email: "",
      to_name: "friend",
      from_name: "Test site",
      test_message: "test message"
    };
  },
  mounted() {
    // let externalScript = document.createElement('script')
    // externalScript.setAttribute('src', 'https://smtpjs.com/v3/smtp.js')
    // document.head.appendChild(externalScript)
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
  methods: {
    sendEmail() {
      console.log("here I am", this.$refs.form)

        emailjs.sendForm('service_jkcv4ow', 'template_v7ssima', 
        this.$refs.form,
          '47VzS0YlF3iktUPQt')
        .then((result) => {
            console.log('SUCCESS!', result.text);
            
      
        }, (error) => {
            console.log('FAILED...', error.text);
        });
        
    },

    handleSubscribe() {
      console.log( this.sub_email);
      
      this.to_name = "friend";
      this.from_name = "Test site"

      this.test_message = "test message";
      this.sendEmail();
     

      // console.log(Email);
      // Email.send({
      //     Host : "smtp.mailtrap.io",
      //     Username : "69a5a5b0039230",
      //     Password : "935b3276d167d9",
      //     To : 'talenteddev9989@gmail.com',
      //     From : "talenteddev9989@gmail.com",
      //     Subject : "Test email",
      //     Body : "<html><h2>Header</h2><strong>Bold text</strong><br></br><em>Italic</em></html>"
      // }).then(
      //   message => alert(message)
      // );

      // UserService.getSubScribe().then(  
      //   (response) => {
      //     console.log(response);
      //   // this.content = response.data;
      // },
      // (error) => {
      //   console.log(error);
      //   // this.content =
      //   //   (error.response &&
      //   //     error.response.data &&
      //   //     error.response.data.message) ||
      //   //   error.message ||
      //   //   error.toString();
      // })
      emailjs.sendForm('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', this.$refs.form, 'YOUR_PUBLIC_KEY')
        .then((result) => {
            console.log('SUCCESS!', result.text);
        }, (error) => {
            console.log('FAILED...', error.text);
        });
    }
  },
};
</script>
