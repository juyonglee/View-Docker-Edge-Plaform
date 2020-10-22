<template>
  <div>
    <div class="header pb-8 pt-5 pt-lg-8 d-flex align-items-center profile-header" style="min-height: 300px; background-image: url(img/theme/profile-cover.jpg); background-size: cover; background-position: center top;">
      <b-container fluid>
        <!-- Mask -->
        <span class="mask bg-gradient-success opacity-8"></span>
        <!-- Header container -->
        <b-container fluid class="d-flex align-items-center">
          <b-row>
            <b-col xl="6" md="12">
              <h1 class="display-2 text-white">WBC Table 생성</h1>
              <p class="text-white mt-0 mb-5">사용자가 White Box Cryptography를 사용하기 위해서는 암호화 및 복호화 테이블을 생성하는 과정을 수행해야 합니다.</p>
            </b-col>
            <b-col xl="6" class="mt-2">
              <b-table head-variant="light" hover :fields="algorithm.fields" :items="algorithm.items" :caption-top="position"></b-table>
            </b-col>
          </b-row>
        </b-container>
      </b-container>
    </div>
    <!-- WBC Table 생성 Form -->
    <b-container fluid class="mt--6">
      <b-row>
        <b-col xl="4" class="order-xl-2 mb-5">
          <b-card no-body class="card-profile" alt="Image placeholder" img-top>
            <b-row class="justify-content-center">
              <b-col lg="3" class="order-lg-2">
                <div class="card-profile-image">
                  <a href="#">
                    <b-img src="img/theme/team-4.jpg" rounded="circle" />
                  </a>
                </div>
              </b-col>
            </b-row>
            <b-card-header class="text-center border-0 pt-8 pt-md-4 pb-0 pb-md-4"></b-card-header>
            <b-card-body class="pt-0">
              <b-row>
                <b-col>
                  <div class="card-profile-stats d-flex justify-content-center mt-md-5">
                    <div>
                      <span class="heading">AES</span>
                      <span class="description">Algorithm</span>
                    </div>
                    <div>
                      <span class="heading">128bit</span>
                      <span class="description">Size</span>
                    </div>
                    <div>
                      <span class="heading">CBC</span>
                      <span class="description">Mode</span>
                    </div>
                  </div>
                </b-col>
              </b-row>
              <div class="text-center">
                <h5 class="h3">WBC</h5>
                <div class="h5 font-weight-300">
                  <i class="ni location_pin mr-2"></i>Bucharest, Romania
                </div>
                <div class="h5 mt-4">
                  <i class="ni business_briefcase-24 mr-2"></i>Seed - {{generate_option.seed}}
                </div>
                <div class="h5 mt-4">
                  <i class="ni business_briefcase-24 mr-2"></i>Master Key - {{generate_option.masterKey}}
                </div>
                <div>
                  <i class="ni education_hat mr-2"></i>University of Computer Science
                </div>
              </div>
    </b-card-body>
  </b-card>
          
        </b-col>
        <!-- WBC Table 생성 입력 Form -->
        <b-col xl="8" class="order-xl-1">
          <card>
            <b-row align-v="center" slot="header">
              <b-col cols="8">
                <h3 class="mb-0">WBC Table 생성</h3>
              </b-col>
            </b-row>
            <b-form @submit.prevent="updateProfile">
              <h6 class="heading-small mb-4">WBC Algorithm</h6>
              <div class="pl-lg-4">
                 <b-col lg="6" class="ml-1">
                    <multiselect v-model="generate_option.algoOp" :options="algorithm.items" label="algorithm" :allow-empty="false" :close-on-select="true"></multiselect>
                  </b-col>
              </div>
              <!-- <b-row>
                  <b-col lg="6">
                    <h6 class="heading-small mb-4">WBC Algorithm 선택</h6>
                    <multiselect v-model="generate_option.algoOp" :options="algorithm.items" label="algorithm" :allow-empty="false" :close-on-select="true"></multiselect>
                  </b-col>
                  <b-col lg="6">
                    <h6 class="heading-small mb-4">WBC Algorithm 선택</h6>
                    <multiselect v-model="generate_option.algoOp" :options="algorithm.items" label="algorithm" :allow-empty="false" :close-on-select="true"></multiselect>
                  </b-col>
              </b-row> -->
              <hr class="my-4">
              <!-- WBC Table 생성 옵션 -->
              <h6 class="heading-small mb-4">Seed & Master Key</h6>
              <div class="pl-lg-4">
                <b-row>
                  <b-col lg="12">
                    <base-input
                      alternative class="mb-3" 
                      name="Master Key"
                      :rules="{required: true, min: 10, max:10}"
                      prepend-icon="ni ni-key-25"
                      type="text"
                      placeholder="Master Key를 입력해주세요."
                      v-model="generate_option.masterKey">
                    </base-input>
                  </b-col>
                </b-row>
                <b-row>
                  <b-col lg="12">
                    <!-- <base-input type="text" label="Seed" placeholder="Seed를 입력해주세요." v-model="generate_option.seed"></base-input> -->
                    <base-input alternative
                              class="mb-3"
                              name="Seed"
                              :rules="{required: true, min: 6}"
                              prepend-icon="ni ni-lock-circle-open"
                              type="text"
                              placeholder="Seed를 입력해주세요."
                              v-model="generate_option.seed">
                    </base-input>
                  </b-col>
                </b-row>
              </div>
              <hr class="my-4">
              <b-nav class="nav-pills justify-content-end">
                <base-button icon type="primary" v-on:click="create_table">
                  <span class="btn-inner--icon"><i class="ni ni-bag-17"></i></span>
                  <span class="btn-inner--text">Table 생성</span>
                </base-button>
              </b-nav>              
      <!-- <b-form-textarea rows="4" value="A beautiful premium dashboard for BootstrapVue." id="about-form-textaria" placeholder="A few words about you ..."></b-form-textarea> -->
            </b-form>
          </card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
  import Multiselect from 'vue-multiselect'

  export default {
    components: {
      Multiselect
    },
    methods: {
      create_table() {
        alert(this.generate_option.algoOp.option)
        alert(this.generate_option.seed)
        alert(this.generate_option.masterKey)
      }
    },
    data() {
      return {
        test: null,
        generate_option: {
          algoOp: '',
          seed: '12312341243513462354634',
          masterKey: '47477C56567A4F8434CFE1774F295102'
        },
        position: true,
        items: [
          { age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
          { age: 21, first_name: 'Larsen', last_name: 'Shaw' },
          { age: 89, first_name: 'Geneva', last_name: 'Wilson' },
          { age: 38, first_name: 'Jami', last_name: 'Carney' }
        ],
        algorithm: {
          fields: [
            { key: 'algorithm', label: 'Algorithm', class: 'text-center'},
            { key: 'size', label: 'Size', class: 'text-center'},
            { key: 'option', label: 'Option', class: 'text-center'},
            { key: 'mode', label: 'Mode', class: 'text-center'}
          ],
          items: [
            { algorithm: 'AES', size: "128bit", option: 'AES128', mode: 'CBC, ECB'},
            { algorithm: 'ARIA', size: "128bit", option: 'ARIA_32_128', mode: 'CBC, ECB'},
            { algorithm: 'LEA', size: "128bit", option: 'LEA128', mode: 'CBC, ECB'}
          ]
        }
      }
    },
    created() {
      if(this.algorithm.items.length != 0) {
        this.generate_option.algoOp = this.algorithm.items[0]
      }
    }
  };
</script>
<style></style>
<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
