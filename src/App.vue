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
                    v-model="search"
                    aria-describedby="helpId"
                    placeholder="Name"
                  />
                </div>
              </div>
              <button
                type="button"
                class="btn btn-primary m-1"
                v-on:click="btnLabel = 'doubleIncome'"
              >
                Double Income
              </button>
              <button
                type="button"
                class="btn btn-primary m-1"
                v-on:click="btnLabel = 'showOnlyMillionaries'"
              >
                Show only Millionaires
              </button>
              <button
                type="button"
                class="btn btn-primary m-1"
                v-on:click="btnLabel = 'incomplete'"
              >
                Show only Incomplete
              </button>
              <button
                type="button"
                class="btn btn-primary m-1"
                v-on:click="btnLabel = 'riches'"
              >
                Sort by Richest
              </button>
              <button
                type="button"
                class="btn btn-primary m-1"
                v-on:click="btnLabel = 'sortfromlowincome'"
              >
                From Low Income to Up
              </button>
              <button
                type="button"
                class="btn btn-primary m-1"
                v-on:click="btnLabel = 'total'"
              >
                Calculate Total Income
              </button>
            </div>
          </div>
          <div class="col" id="mainUsers">
            <div class="d-flex justify-content-between mb-2">
              <div class="font-weight-bold ml-3">Users</div>
              <div class="font-weight-bold ml-auto">Income(MMK)</div>
            </div>
            <template v-if="filterUser.length">
              <div
                class="d-flex justify-content-between mb-2"
                v-for="(user, index) in filterUser"
                v-bind:key="index"
              >
                <div class="ml-3">{{ user.name }}</div>
                <div class="ml-auto">{{ formatNumberMMK(user.income) }}</div>
              </div>
              <div class="d-flex justify-content-between mb-2" v-if="total > 0">
                <div class="font-weight-bold">Total</div>
                <div class="font-weight-bold">{{ formatNumberMMK(total) }}</div>
              </div>
            </template>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
//defalut name UserRepo
import UserRepo from "./userRepo";
export default {
  name: "App",
  data: () => ({
    title: "従業員の給料アレイ",
    explain: "(Employees' Array Income)",
    users: UserRepo,
    btnLabel: "",
    total: 0,
    search: "",
  }),
  created() {
    this.users = this.users.map((user) => {
      return {
        name: user.name,
        income: Math.floor(Math.random() * 1000000),
      };
    });
  },
  methods: {
    formatNumberMMK(num) {
      return Number(num).toLocaleString("mmk");
    },
    setBtnLabel(val) {
      this.btnLabel = val;
    },
    setUsers(val) {
      this.users = val;
    },
    setTotal(val) {
      this.total = val;
    },
  },
  computed: {
    //method with return
    filterUser() {
      let tmp = this.users;
      this.setTotal(0);
      if (this.btnLabel == "doubleIncome") {
        tmp = tmp.map((user) => {
          //return as object
          return {
            name: user.name,
            income: user.income * 2,
          };
        });
        this.setUsers(tmp);
        this.setBtnLabel("");
      } else if (this.btnLabel == "showOnlyMillionaries") {
        tmp = tmp.filter((user) => {
          return user.income > 1000000;
        });
      } else if (this.btnLabel == "incomplete") {
        tmp = tmp.filter((user) => {
          return user.income < 1000000;
        });
      } else if (this.btnLabel == "riches") {
        tmp = tmp.sort((a, b) => {
          return b.income - a.income;
        });
      } else if (this.btnLabel == "sortfromlowincome") {
        tmp = tmp.sort((a, b) => {
          return a.income - b.income;
        });
      } else if (this.btnLabel == "total") {
        let dataKyat = tmp.reduce(
          (total, user) => (total += Number(user.income)),
          0
        );
        this.setTotal(dataKyat);
      } else if (this.search !== "") {
        let search = this.search.toLowerCase();
        if (search) {
          tmp = tmp.filter((v) => v.name.toLowerCase().indexOf(search) > -1);
        }
      }
      return tmp;
    },
  },
};
</script>

<style>
body {
  background-color: #948957 !important;
}
</style>
