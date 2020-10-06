<template>
<v-container>
  <v-row>
    <v-col cols="12" md="12">
      <v-card color="basil">
        <v-card-title class="py-6">
          <v-container>
            <v-row>
              <v-col cols="12" md="7">
                <h1 style="float: right;">Buy &amp; sell stocks</h1>
              </v-col>
              <v-col cols="12" md="5">
                <p style="float: right; padding-left: 3%;">Account: ${{ account }}</p>
                <v-btn style="float: right;" @click="ResetDay">
                  End Day
                </v-btn>
              </v-col>
            </v-row>
          </v-container>
        </v-card-title>

        <v-tabs
          v-model="tab"
          background-color="transparent"
          color="basil"
          grow
        >
          <v-tab
          >
          <p>Buy</p>
          </v-tab>
          <v-tab
          >
          <p>Inventory</p>
          </v-tab>
        </v-tabs>

        <v-tabs-items v-model="tab">
          <v-tab-item
          >
            <v-card
              color="basil"
              flat
            >
              <v-container>
              <v-row>
                <v-col
                  cols="12"
                  md="3"
                >
                <v-card
                    max-width="364"
                    class="mx-auto"
                  >
                    <v-list-item>
                      <v-list-item-content>
                        <v-list-item-title class="text-center">BMW</v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>
                    <v-card-text>
                      <v-text-field
                        type="number"
                        v-model="BMW"
                        label="BMW"
                        required
                      ></v-text-field>
                    </v-card-text>

                    <v-card-actions>
                      <v-btn
                        @click="updateAccountInfo('BMW')"
                        class="primary"
                      >
                        Buy
                      </v-btn>
                      <p class="text-right">Price: {{ BMWprice }}</p>
                    </v-card-actions>
                  </v-card>
                </v-col>
                <v-col
                  cols="12"
                  md="3"
                >
                  <v-card
                    max-width="364"
                    class="mx-auto"
                  >
                    <v-list-item>
                      <v-list-item-content>
                        <v-list-item-title class="text-center">Apple</v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>
                    <v-card-text>
                      <v-text-field
                        type="number"
                        v-model="Apple"
                        label="Apple"
                        required
                      ></v-text-field>
                    </v-card-text>

                    <v-card-actions>
                      <v-btn 
                        @click="updateAccountInfo('Apple')"
                        class="primary"
                      >
                        Buy
                      </v-btn>
                      <p class="text-right">Price: {{ Appleprice }}</p>
                    </v-card-actions>
                  </v-card>
                </v-col>

                <v-col
                  cols="12"
                  md="3"
                >
                  <v-card
                    max-width="364"
                    class="mx-auto"
                  >
                    <v-list-item>
                      <v-list-item-content>
                        <v-list-item-title class="text-center">GoPro</v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>
                    <v-card-text>
                      <v-text-field
                        type="number"
                        v-model="GoPro"
                        label="GoPro"
                        required
                      ></v-text-field>
                    </v-card-text>

                    <v-card-actions>
                      <v-btn 
                        @click="updateAccountInfo('GoPro')"
                        class="primary"
                      >
                        Buy
                      </v-btn>
                      <p class="text-right">Price: {{ GoProprice }}</p>
                    </v-card-actions>
                  </v-card>
                </v-col>

                <v-col
                  cols="12"
                  md="3"
                >
                  <v-card
                    max-width="364"
                    class="mx-auto"
                  >
                    <v-list-item>
                      <v-list-item-content>
                        <v-list-item-title class="text-center">Facebook</v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>
                    <v-card-text>
                      <v-text-field
                        type="number"
                        v-model="Facebook"
                        label="Facebook"
                        required
                      ></v-text-field>
                    </v-card-text>

                    <v-card-actions>
                      <v-btn
                        @click="updateAccountInfo('Facebook')"
                        class="primary"
                      >
                        Buy
                      </v-btn>
                      <p class="text-right">Price: {{ Facebookprice }}</p>
                    </v-card-actions>
                  </v-card>
                </v-col>
              </v-row>
            </v-container>
            </v-card>
          </v-tab-item>
          <v-tab-item
          >
            <v-card
              color="basil"
              flat
            >
              <v-container>
                <v-row>
                  <v-col cols="12" v-if="emptyState()">
                    <h3 class="text-center">Inventory is empty</h3>
                  </v-col>
                  <v-col v-for="(shares, companyName, idx) in purchedStocks" :key="idx">
                    <v-card
                      max-width="364"
                      class="mx-auto"
                      v-if="purchedStocks[companyName] > 0"
                    >
                      <v-list-item>
                        <v-list-item-avatar color="grey"></v-list-item-avatar>
                        <v-list-item-content>
                          <v-list-item-title class="headline">Our Changing Planet</v-list-item-title>
                          <v-list-item-subtitle>by Kurt Wagner</v-list-item-subtitle>
                        </v-list-item-content>
                      </v-list-item>
                      <v-card-text>
                        {{ shares }} {{ companyName }}
                        <v-text-field
                          type="number"
                          :id="companyName + '_' + 'share'"
                          label="GoPro"
                          required
                        ></v-text-field>
                      </v-card-text>

                      <v-card-actions>
                        <v-btn @click="sell(companyName)">Sell</v-btn>
                      </v-card-actions>
                    </v-card>
                  </v-col>
                </v-row>
              </v-container>
            </v-card>
          </v-tab-item>
        </v-tabs-items>
      </v-card>
    </v-col>
    <v-col cols="12">
      <h3>Initially you'll be provided $100, Buy and sell the stocks with them after the days ends(you can end day with the button at the top)</h3>
    </v-col>
    <v-col>
      <h1 class="text-center">
        Made by: Nitesh Poonia
      </h1>
    </v-col>
  </v-row>
</v-container>
</template>
<script>
export default {
  data: () => ({
    tab: null,
    Apple: "",
    GoPro: "",
    Facebook: "",
    BMW: "",
    BMWprice: 2,
    purchedStocks: {
      BMW: 0,
      Apple: 0,
      GoPro: 0,
      Facebook: 0
    },
    Appleprice: 2,
    GoProprice: 2,
    Facebookprice: 2,
    account: 100,
    movie: {}
  }),
  mounted () {
    this.ResetDay()
  },
  methods: {
    updateAccountInfo (company) {
      if (this.Apple === "" && this.BMW === "" && this.Facebook === "" && this.GoPro === "") {
        return
      }
      if (company === "BMW") {
        this.account = this.account - this.BMW * this.BMWprice
        this.purchedStocks.BMW += parseInt(this.BMW)
        this.BMW = ""
      } else if (company === "Apple") {
        this.account = this.account - this.Apple * this.Appleprice
        this.purchedStocks.Apple += parseInt(this.Apple)
        this.Apple = ""
      } else if (company === "GoPro") {
        this.account = this.account - this.GoPro * this.GoProprice
        this.purchedStocks.GoPro += parseInt(this.GoPro)
        this.GoPro = ""
      } else if (company === "Facebook") {
        this.account = this.account - this.Facebook * this.Facebookprice
        this.purchedStocks.Facebook += parseInt(this.Facebook)
        this.Facebook = ""
      }
    },
    ResetDay () {
      this.BMWprice = Math.floor(Math.random() * 11) + 6
      this.Appleprice = Math.floor(Math.random() * 11) + 6
      this.GoProprice = Math.floor(Math.random() * 11) + 6
      this.Facebookprice = Math.floor(Math.random() * 11) + 6
    },
    sell (company) {
      const share = document.getElementById(company + "_" + "share").value
      if (company === "BMW") {
        this.account += this.BMWprice * parseInt(share)
        this.purchedStocks.BMW -= parseInt(share)
      } else if (company === "Apple") {
        this.account += this.Appleprice * parseInt(share)
        this.purchedStocks.Apple -= parseInt(share)
      } else if (company === "GoPro") {
        this.account += this.GoProprice * parseInt(share)
        this.purchedStocks.GoPro -= parseInt(share)
      } else if (company === "Facebook") {
        this.account += this.Facebookprice * parseInt(share)
        this.purchedStocks.Facebook -= parseInt(share)
      }
      document.getElementById(company + "_" + "share").value = ""
    },
    emptyState () {
      let sum = 0
      Object.keys(this.purchedStocks).map((key) => {
        sum += this.purchedStocks[key]
      })
      return sum === 0
    }
  }
}
</script>

<style>
.basil {
  background-color: #FFFBE6 !important;
}
.basil--text {
  color: #356859 !important;
}
.text-center {
  text-align: center;
}
.text-right {
  padding-left: 54%
}
.primary {
  background-color: #6adf4d !important;
  color: white;
}
.primary:hover {
  background-color: #33ff00 !important;
  color: white;
}
</style>
