<script setup>
import IconFirstStep from './icons/IconFirstStep.vue';
import SelectInput from "@/components/Form/SelectInput.vue";
import NextButton from "@/components/Form/NextButton.vue";
import PrevButton from "@/components/Form/PrevButton.vue";
import Step from "@/components/Step.vue";
import SupplyIcon from "@/components/icons/SupplyIcon.vue";
import MarketIcon from "@/components/icons/MarketIcon.vue";
import TextInput from "@/components/Form/TextInput.vue";
import Checkbox from "@/components/Form/Checkbox.vue";
import CheckIcon from "@/components/icons/CheckIcon.vue";
</script>
<template>
  <Step :class="{'second-step': step == 2, 'third-step': step == 3 }"/>
  <div class="wrapper white-bg padding-rectangle" v-if="step == 1">
    <div class="container">
      <div class="row align-items-center">
        <div class="col-12 col-md-12 col-lg-6">
          <IconFirstStep/>
        </div>
        <div class="col-12 col-md-12 col-lg-6">
          <div class="wrapper-description">
            <h3>Merhaba...</h3>
            <p>Mağazanızı oluşturmak için alış ve satış kaynaklarını seçebilirsin.</p>
          </div>
          <SelectInput :data="market" title="Kaynak Mağaza" description="Açıklama" name="sourceMarket"/>
          <SelectInput :data="market" title="Hedef Mağaza" description="Açıklama" name="targetMarket"/>
        </div>
      </div>
      <div class="row justify-content-between btn-row">
        <div class="col-6 col-md-4 col-lg-3 text-start">
          <PrevButton @click="step--" :disabled="step==1"/>
        </div>
        <div class="col-6 col-md-4 col-lg-3 text-end">
          <NextButton @click="step++" :disabled="step==3"/>
        </div>
      </div>
    </div>
  </div>
  <div class="wrapper" v-if="step == 2">
    <div class="container">
      <div class="row">
        <div class="col-12 col-md-12 col-lg-6">
          <div class="wrapper-tabs">
            <ul>
              <li v-on:click="activetab=1" v-bind:class="[ activetab === 1 ? 'active' : '' ]">
                Temel Ayarlar
              </li>
              <li v-on:click="activetab=2" v-bind:class="[ activetab === 2 ? 'active' : '' ]">
                Gelişmiş
              </li>
              <li v-on:click="activetab=3" v-bind:class="[ activetab === 3 ? 'active' : '' ]">
                Ultra
              </li>
            </ul>
          </div>
          <div class="white-bg white-bg padding-square active-wrapper">
            <div class="wrapper-description">
              <SupplyIcon/>
              <div class="wrapper-description-title">
                <h4>Genel Tedarikçi Ayarları <i class="fa-solid fa-circle-info"></i></h4>
              </div>
            </div>
            <TextInput title="Ekstra Vergi Ortalaması" description="Ekstra vergi ortalaması" name="tax"
                       iconType="fa-light fa-percent"/>
            <div class="fancy">
              <span></span>
            </div>
            <Checkbox title="İndirimli fiyatı kullan." name="discount"/>
            <div class="button-row text-start">
              <PrevButton @click="step--" :disabled="step==1"/>
            </div>
          </div>
        </div>
        <div class="col-12 col-md-12 col-lg-6">
          <div class="white-bg white-bg padding-square">
            <div class="wrapper-description">
              <MarketIcon/>
              <div class="wrapper-description-title">
                <h4>Genel Mağaza Ayarları <i class="fa-solid fa-circle-info"></i></h4>
              </div>
            </div>
            <div class="row align-items-center input-row">
              <div class="col-12 col-lg-7">
                <TextInput title="Ülke Döviz Kuru (1 USD)" description="Ülke döviz kuru (1 USD)" name="tax"
                           iconType="fa-solid fa-dollar-sign"/>
              </div>
              <div class="col-12 col-lg-1">
                <span class="or">veya</span>
              </div>
              <div class="col-12 col-lg-4">
                <Checkbox title="Otomatik" name="auto"/>
              </div>
            </div>
            <div class="fancy">
              <span></span>
            </div>
            <div class="row align-items-end input-row text-input-group">
              <div class="col-12 col-lg-5">
                <TextInput title="Minimum Kar Oranı Veya Tutarı" description="Minimum kar oranı veya tutarı"
                           name="profit" iconType="fa-light fa-percent"/>
              </div>
              <div class="col-12 col-lg-2">
                <span class="or">ve</span>
              </div>
              <div class="col-12 col-lg-5">
                <TextInput name="gain" iconType="fa-solid fa-dollar-sign"/>
              </div>
            </div>
            <div class="button-row text-end">
              <NextButton @click="step++" :disabled="step==3"/>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="wrapper white-bg padding-rectangle success-screen" v-if="step == 3">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <div class="wrapper-description">
            <CheckIcon/>
            <h4>Kurulum Tamamlandı</h4>
            <p>Lorem Ipsum, dizgi ve baskı endüstrisinde kullanılan mıgır metinlerdir.</p>
            <a href="/" class="btn blue">Ana Ekrana Git <i class="fa-solid fa-arrow-right"></i></a>
            <span>{{ timerCount }} sn. sonra yönlendirileceksiniz.</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Wrapper",
  data() {
    return {
      market: [],
      step: 1,
      tabs: ['Temel Ayarlar', 'Gelişmiş', 'Ultra'],
      activetab: 1,
      timerCount: 10
    };
  },
  methods: {
    countDown() {
      //If the counter has not reached the end
      if(this.timerCount > 0) {
        //Wait 1 second, then decrement the counter
        setTimeout(()=>{
          this.timerCount--;
          this.countDown();
        },1000)
      }
      else
      {
        //Count down has reached zero, redirect
        window.location.href = '/';
      }
    },
  },
  watch: {
    step(step){
      if (step === 3){
        this.countDown();
      }
    }
  },
  async created() {
    try {
      const res = await axios.get(`http://api.worldbank.org/v2/country?format=json`);
      this.market = res.data[1];
    } catch (e) {
      console.error(e);
    }
  }
};

</script>