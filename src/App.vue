<template>
  <div>
    <h5 class="bg-primary text-white text-center font-weight-bold p-3">
      {{ title }} {{ explain }}
    </h5>
    <div class="container">
      <div class="card p-3">
        <div class="row">
          <div class="col-5">
            <div class="d-flex flex-column">
              <div class="p-1">
                <div class="form-group p-2">
                  <label for="Search" class="d-block text-center"
                    >Search by Name</label
                  >
                  <input
                    type="text"
                    class="form-control"
                    name="Search"
                    id="search"
                    aria-describedby="helpId"
                    placeholder="Name"
                  />
                </div>
              </div>
              <button type="button" class="btn btn-primary m-1" v-on:click="doubleIncome">
                Double Income
              </button>
              <button
                type="button"
                class="btn btn-primary m-1"
                v-on:click="showOnlyMillionaries"
              >
                Show only Millionaires
              </button>
              <button type="button" class="btn btn-primary m-1" v-on:click="incomplete">
                Show only Incomplete
              </button>
              <button type="button" class="btn btn-primary m-1" v-on:click="riches">
                Sort by Richest
              </button>
              <button
                type="button"
                class="btn btn-primary m-1"
                v-on:click="sortfromlowincome"
              >
                From Low Income to Up
              </button>
              <button type="button" class="btn btn-primary m-1" id="total">
                Calculate Total Income
              </button>
            </div>
          </div>
          <div class="col" id="mainUsers">
            <div class="d-flex justify-content-between mb-2">
              <div class="font-weight-bold ml-3">Users</div>
              <div class="font-weight-bold ml-auto">Income(MMK)</div>
              <div class="font-weight-bold ml-auto">Edit/Delete</div>
            </div>
            <template v-if="filterUser.length">
              <div
              class="d-flex justify-content-between mb-2"
              v-for="(user, index) in filterUser"
              v-bind:key="index"
            >
              <div class="ml-3">{{ user.name }}</div>
              <div class="ml-auto">{{formatNumberMMK(user.income)}}</div>
              <div class="ml-auto">Edit/Delete</div>
            </div>
            </template>
            
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    title: "従業員の給料アレイ",
    explain: "(Employees' Array Income)",
    users: [
      {
        name: "Kyaw Kyaw",
      },
      {
        name: "Su Su Aye Aung",
      },
      {
        name: "Zaw Myo Tun",
      },
      {
        name: "Thuzar Phyo",
      },
      {
        name: "Kalayar Htun",
      },
      {
        name: "Chan Chan",
      },
      {
        name: "Aung Aung Oo",
      },
      {
        name: "Hsu Mon Aung",
      },
      {
        name: "Kyaw Ye Lwin",
      },
      {
        name: "Wai Phyoe Aung",
      },
    ],
  }),
  computed:{
    filterUser(){
      return this.users.length !== 0 ? this.users.filter(()=> this.users) : this.data;
    }
  },
  methods: {
    formatNumberMMK(num) {
      return Number(num).toLocaleString("mmk");
    },
    storeData() {
      localStorage.setItem("users", JSON.stringify(this.users));
    },
    doubleIncome() {
      //alert('eea')
      this.users = this.users.map((user) => {
        //return as object
        return {
            name: user.name,
            income: user.income * 2
        }
    });
    this.storeData();
    },
    showOnlyMillionaries() {
     // alert('eea')
      this.users = this.users.filter((user) => {
        
          return (user.income > 1000000)
    
    });
    this.users;
      
    },
    incomplete() {
      this.users = this.users.filter((user) => {
        
          return (user.income < 1000000)
        
    });
    this.users;
    },
    riches() {
      this.users = this.users.sort((a, b) => {
        return b.income - a.income
    });
    this.storeData();
    },
    sortfromlowincome() {
      this.users = this.users.sort((a, b) => {
        return a.income - b.income;
    });
    this.storeData();
    }
  },
  created() {  
      this.users = this.users.map((user) => {
    return {
              name: user.name,
              income: Math.floor(Math.random() * 1000000),
             } 
    });
   this.storeData();
},
mounted() {
    let data = localStorage.getItem("users");
      if (data !== null) {
        this.users = JSON.parse(data);
      }  
},
}
</script>

<style>
</style>

