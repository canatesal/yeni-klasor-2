<template>
  <div id="app">
    <!-- Giriş Ekranı -->
    <div v-if="!isLoggedIn" class="login">
      <h1>Blogbook</h1>
      <v-container>
        <v-text-field
          v-model="username"
          label="Kullanıcı Adı"
          outlined
        ></v-text-field>
        <v-text-field
          v-model="password"
          label="Şifre"
          type="password"
          outlined
        ></v-text-field>
        <v-btn color="green" @click="login">Giriş Yap</v-btn>
        <p v-if="errorMessage" class="error">{{ errorMessage }}</p>
      </v-container>
    </div>

    <!-- Blog Sayfası -->
    <div v-else class="blog">
      <header class="blog-header">
        <h1>Blogbook</h1>
      </header>
      <v-container>
        <h2>Yazdığın Bloglar</h2>
        <v-btn color="blue" @click="toggleTextbox">Yeni Blog Yaz</v-btn>
        <!-- Gizli Textbox -->
        <div v-if="showTextbox" class="new-blog">
          <v-textarea
            v-model="newBlog"
            label="Blog Yazınızı Girin"
            outlined
          ></v-textarea>
          <v-btn color="green" @click="addBlog">Yaz</v-btn>
        </div>
        <!-- Blog Listesi -->
        <div v-for="(blog, index) in blogs" :key="index" class="blog-item">
          <p>{{ blog }}</p>
        </div>
      </v-container>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // Login Bilgileri
      isLoggedIn: false,
      username: "",
      password: "",
      errorMessage: "",

      // Blog Bilgileri
      showTextbox: false,
      newBlog: "",
      blogs: [],
    };
  },
  methods: {
    login() {
      // Giriş Kontrolü
      if (this.username === "cagri" && this.password === "1234") {
        this.isLoggedIn = true;
        this.errorMessage = "";
      } else {
        this.errorMessage = "Hatalı kullanıcı adı veya şifre.";
      }
    },
    toggleTextbox() {
      this.showTextbox = !this.showTextbox;
    },
    addBlog() {
      if (this.newBlog.trim() !== "") {
        this.blogs.push(this.newBlog);
        this.newBlog = "";
        this.showTextbox = false;
      }
    },
  },
};
</script>

<style scoped>
/* Genel Stiller */
body {
  font-family: 'Tahoma', sans-serif;
  background-color: #f9f9f9;
  margin: 0;
  padding: 0;
}

/* Giriş Ekranı */
.login {
  text-align: center;
  margin-top: 100px;
}
.login h1 {
  color: #ffffff;
  background-color: #3b82f6;
  padding: 10px;
  border-radius: 5px;
  display: inline-block;
}
.error {
  color: red;
  font-size: 14px;
}

/* Blog Sayfası */
.blog-header {
  text-align: center;
  background: #3b82f6;
  color: white;
  padding: 20px;
  border-radius: 5px;
}
.new-blog {
  margin: 20px 0;
}
.blog-item {
  margin: 10px 0;
  padding: 15px;
  background: white;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}
</style>
