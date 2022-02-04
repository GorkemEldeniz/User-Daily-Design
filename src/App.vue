<template>
    <div class="main">
      <h1>Users</h1>
      <div class="nav">
        <input type="text" placeholder="Search users" maxlength="10" @keyup="search" v-model="param">
        <ol class="sub-nav" @click="check">
          <li>Reputation</li>
          <li>New users</li>
          <li>Voters</li>
          <li>Editors</li>
          <li>Moderators</li>
        </ol>
      </div>

      <div class="content">
          <div class="cards" v-for="data in datas" :key="data">
            <img :src="require(`${data?.pic}`)" :alt="data.name" v-if="data.active">
            <div class="article" v-if="data.active">
              <h2>{{data.name}}</h2>
              <span class="local">{{data.location}}</span>
                <Hobbies :likes="data.hobbies"/>
            </div>
          </div>
      </div>
    </div>
</template>

<script>
import db from './db.js';
import Hobbies from './components/Hobbies.vue'
export default {
  name: 'App',
  components :{
    Hobbies
  },
  data(){
    return{
      datas : null,
      param : null
    }
  },
  created(){
    this.datas = db;
  },
  methods :{
    search(){
      this.datas.forEach(el => {
        el.active = false;
        if(el.name.toLowerCase().includes(this.param.toLowerCase())){
          el.active = true;
        }
      })
    },
    check(e){
      const els = document.querySelectorAll(".sub-nav li");
      els.forEach(el => el.classList.remove('active'));
      e.target.classList.add('active')
    }
  }
}
</script>

<style lang="scss" scoped>
  .main{
    padding:6.25rem;
    display: flex;
    flex-direction: column;
    max-width:90%;
    h1{
      color:#151B32;
      font-family: Merriweather;
      font-size: 2rem;
      line-height: 2.5rem;
      margin-bottom:1.5rem;
    }
    .nav{
      display: flex;
      justify-content: space-between;
      margin-bottom:4.375rem;
      input{
        padding:1rem 3.5rem;
        height:4rem;
        width:20rem;
        border: 1px solid #BFC8E6;
        border-radius: 4px;
        font-family: Poppins;
        font-size:1rem;
        line-height:1.5rem;
        background:url('./assets/search.svg');
        background-repeat:no-repeat;
        background-size:2rem 2rem;
        background-position:1rem 1rem;
      }
      .sub-nav{
        display: flex;
        li{
          transition:all 300ms ease;
          height: 3.5rem;
          cursor:pointer;
          padding:1rem;
          font-family: Poppins;
          font-size:1rem;
          line-height: 1.5rem;
          border-radius: 8px;
          border:1px solid #BFC8E6;
          width: 8.75rem;
          text-align: center;
        }
      }
    }
    .content{
      display: grid;
      grid-template-columns:1fr 1fr 1fr;
      width:100%;
      gap:1rem;
      .cards{
        height: 12.5rem;
        align-items: center;
        padding: 1.5rem;
        display: flex;
        gap:1rem;          
        background: #FBFCFF;
        border: 1px solid #BFC8E6;
        transition:box-shadow 300ms ease;
        border-radius: 16px;
        &:hover{
          box-shadow: 0px 8px 23px rgba(218, 224, 249, 0.7);
        }
        img{
          border-radius: 50%;
          width: 6rem;
          height: 6rem;
        }
        .article{
          display: flex;
          flex-direction: column;
          padding-top:1.2rem;
          h2{
            font-family: Merriweather;
            color:#151B32;
            font-size:1.1rem;
            line-height: 1.3rem;
          }
          .local{
            font-family: Poppins;
            font-style: normal;
            font-weight: normal;
            font-size: 0.875rem;
            line-height: 1.313rem;
            margin-top:.4rem;
          }
        }
      }
    }
  }
</style>
