<template>
  <div id="container">
    <div class="monthly-cost">
          <div class="label monthly-cost-label">
              <!-- monthlyCostLabel -->
              {{ config["monthlyCostLabel"] }}
          </div>
          <div class="label monthly-cost-value">
              <!-- monthlyCost + monthlyCostSuffix -->
              {{ getMonthlyCost }}
          </div>
      </div>
      <div class="amount">
          <div class="label amount-label">
              <!-- loanAmountLabel -->
              {{ config["loanAmountLabel"] }}
          </div>
          <div >
              <button @click="() => stepDown('loanAmount')" class="button calculator-button">
                  <span>-</span>
              </button>

              <input class="amount-value" v-model="getCurrentLoanAmount">

              <button @click="() => stepUp('loanAmount')" class="button calculator-button">
                  <span>+</span>
              </button>
          </div>
      </div>

      <div>
          <div class="label repayment-label">
              <!-- repaymentLabel -->
              {{ config["repaymentYearsLabel"] }}
          </div>

          <div>
              <button @click="() => stepDown('repaymentYears')" class="button calculator-button">
                  <span>-</span>
              </button>

              <input class="repayment-value" v-model="getCurrentRepaymentYears">

              <button @click="() => stepUp('repaymentYears')" class="button calculator-button">
                  <span>+</span>
              </button>
          </div>
      </div>

      <div class="">
          <button class="button cta-button">
              <!-- ctaLabel -->
              <span class=cta-label>
                {{ config["ctaLabel"] }}
              </span>
          </button>
      </div>
  </div>
</template>

<script>
/** Loan Constants */
const LOANSTEP = 5000;
const LOANMAX = 600000;
const LOANMIN = 5000;

/** Repayment years Constants */
const YEARSTEP = 1;
const YEARMAX = 15;
const YEARMIN = 1;

export default {
  name: 'Calculator',
  data() {

    /** Sets our Calculator up, with the default values */
    return {
        "currentLoanAmount": 250000,
        "currentRepaymentTime": 14,
        "config": this.getContent()
    };
  },
  computed: {

    /** Returns a pretty string of the current monthly cost */
    getMonthlyCost() {
      return this.calculateMonthlyCost(this.currentRepaymentTime, this.currentLoanAmount) + " " + this.config["monthlyCostSuffix"];
    },

    /** Returns a pretty string of the current loan amount */
    getCurrentLoanAmount() {
      return this.currentLoanAmount.toLocaleString() + " " + this.config["monthlyCostSuffix"]
    },

    /** Returns a pretty string of the current repayment years */
    getCurrentRepaymentYears() {
      return this.currentRepaymentTime + " " + this.config["repaymentYearsSuffix"]
    }
  },

  methods: {

    /**
     * Increases the loan amount or the repayment years
     */
    stepUp(type) {
      switch(type) {
        case "loanAmount":
          if (this.currentLoanAmount + LOANSTEP <= LOANMAX) {
            this.currentLoanAmount += LOANSTEP
          }
          break;
        case "repaymentYears":
          if (this.currentRepaymentTime + YEARSTEP <= YEARMAX) {
            this.currentRepaymentTime += YEARSTEP
          }
          break;
        default:
          return
      }
    },

    /**
     * Decreases the loan amount or the repayment years
     */
    stepDown(type) {
      switch(type) {
        case "loanAmount":
          if (this.currentLoanAmount - LOANSTEP >= LOANMIN) {
            this.currentLoanAmount -= LOANSTEP
          }
          break;
        case "repaymentYears":
          if (this.currentRepaymentTime - YEARSTEP >= YEARMIN) {
            this.currentRepaymentTime -= YEARSTEP
          }
          break;
        default:
          return
      }
    },

  /**
   * Calculates monthly cost of a loan given repayment years and loan amount.
   * Uses an interest value from configuration object.
   */
    calculateMonthlyCost(repaymentYears, loanAmount) {
      let interest = this.config["interest"]
      var months = repaymentYears * 12;

      return Math.round(loanAmount * (interest / 100) / 12 / (1 - Math.pow(1 + (interest / 100) / 12, (months * -1))));
    },

    /**
     * Simulates an API call to a CMS.
     */
    getContent() {
        return {
            "monthlyCostLabel": "Månadskostnad",
            "monthlyCostSuffix": "kr",
            "loanAmountLabel": "Lånebelopp",
            "loanAmountSuffix": "kr",
            "repaymentYearsLabel": "Återbetalningstid",
            "repaymentYearsSuffix": "år",
            "ctaLabel": "Ansök nu",
            "interest": 5.77
        };
    }
  }
}
</script>

<style>
  .calculator-button {
      border-radius: 50%;
      font-size: 40px;
      width: 44px;
  }

  .cta-button {
      border-radius: 22px;
      width: 100%;
      text-align: left;
      margin-top: 15px;
  }

  .cta-label {
    padding-left: 15px;
    font-style: italic;
    font-size: 14px;
  }
  
  .monthly-cost-label {
    font-weight: 600;
  }

  .monthly-cost-value {
      font-size: 20px;
      font-style: italic;
      font-weight: 100;
      
      padding-bottom: 10px;
  }
</style>