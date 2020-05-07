<template>
  <div class="container">
    <div class="form-wrapper general-info">
      <h2 class="form-title general">General Information</h2>
      <form class="form" action>
        <select class="select primary" name="title" id="title">
          <option value disabled selected hidden>Title</option>
          <option value="Businessman">Businessman</option>
          <option value="Secretary">Secretary</option>
          <option value="Reporter">Reporter</option>
        </select>
        <div class="wrapper">
          <input
            class="input primary"
            type="text"
            placeholder="First Name"
            v-model="firstName"
          />
          <input
            class="input primary"
            type="text"
            placeholder="Last Name"
            v-model="lastName"
          />
        </div>
        <select class="select primary" name="position" id="position">
          <option value disabled selected hidden>Position</option>
          <option value="Director">Director</option>
          <option value="Manager">Manager</option>
          <option value="Employee">Employee</option>
        </select>
        <input class="input primary" type="text" placeholder="Company" />
      </form>
    </div>
    <div class="form-wrapper contact-detail">
      <h2 class="form-title contact">Contact Details</h2>
      <form class="form" @submit.prevent="showModal = true">
        <input class="input secondary" type="text" placeholder="Address" />
        <div class="wrapper">
          <input class="input secondary" type="text" placeholder="Zip Code" />
          <div class="wrapper">
            <select class="select secondary" name="place" id="place">
              <option value disabled selected hidden>Place</option>
              <option value="Street">Street</option>
              <option value="District">District</option>
              <option value="City">City</option>
            </select>
          </div>
        </div>
        <select class="select secondary" name="country" id="country">
          <option value disabled selected hidden>Country</option>
          <option v-for="(country, i) in countryList" :key="i">{{
            country.name
          }}</option>
        </select>
        <div class="wrapper">
          <input class="input secondary" type="text" placeholder="Code +" />
          <input
            class="input secondary"
            type="text"
            placeholder="Phone Number"
          />
        </div>
        <input class="input secondary" type="text" placeholder="Your Email" />
        <div class="agreement-wrapper">
          <input
            class="checkbox"
            type="checkbox"
            id="agreement"
            name="agreement"
            value="agree"
          />
          <label class="agreement-label" for="agreement"
            >I do accept the Terms and Conditions of your sites</label
          >
        </div>
        <input class="btn" type="submit" value="Register" />
      </form>
    </div>
    <div v-if="showModal" class="modal">
      <div class="header">
        <p class="modal-title">Register Confirmation</p>
        <i class="material-icons" @click="showModal = false">cancel</i>
      </div>
      <div class="modal-content">
        <ul>
          <li>{{ `FirstName: ${firstName}` }}</li>
          <li>{{ `LastName: ${lastName}` }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    name: "TwisForm",
    data() {
      return {
        countryList: [],
        firstName: "",
        lastName: "",
        showModal: false,
      };
    },
    methods: {
      getCountryList: async function() {
        await axios
          .get("https://restcountries.eu/rest/v2/all")
          .then(res => {
            this.countryList = res.data;
          })
          .catch(err => {
            console.log(err);
          });
      },
    },
    created() {
      this.getCountryList();
    },
  };
</script>

<style lang="scss">
  .container {
    /* position: relative; */
    display: flex;
    flex-direction: column;
    margin: 0 15px;
    border-radius: 5px;
    overflow: hidden;
    opacity: 0.95;
  }

  .modal {
    position: absolute;
    background-color: white;
    bottom: 25%;
    left: 15%;
    border-radius: 3px;
    width: 70vw;
    overflow: hidden;
  }

  .form {
    display: flex;
    flex-direction: column;
  }

  .form-wrapper {
    display: flex;
    padding: 15px;
    flex-direction: column;
  }

  .general-info {
    background-color: white;
  }

  .contact-detail {
    background-color: darkorange;
  }

  .form-title {
    font-weight: lighter;

    &.general {
      color: dodgerblue;
    }

    &.contact {
      color: white;
    }
  }

  .input {
    width: 96%;
    border: none;
    padding: 8px 5px;
    border-bottom: 1px solid black;
    margin: 10px 0 0 5px;
    background-color: transparent;
  }

  .select {
    border: none;
    border-bottom: 1px solid black;
    padding: 8px 0;
    width: 99%;
    background-color: transparent;
    margin: 10px 0 0 5px;
  }

  .btn {
    align-self: center;
    background-color: white;
    border: none;
    font-weight: bold;
    width: fit-content;
    padding: 7px 35px;
    border-radius: 50px;
    margin: 25px 0;
  }

  .agreement-wrapper {
    display: flex;
    margin-top: 10px;
  }

  .checkbox {
    background-color: transparent;
  }

  .agreement-label {
    color: white;
    font-size: 14px;
  }

  .primary {
    color: gray;
    background-color: white;
    border-bottom: 1px solid lightgray;
  }

  .secondary {
    color: white;
    background-color: darkorange;
    border-bottom: 1px solid white;

    &::placeholder {
      color: white;
    }
  }

  @media only screen and (min-width: 768px) {
    .container {
      flex-direction: row;
    }

    .btn {
      align-self: flex-start;
    }

    .form-wrapper {
      padding: 40px;
    }

    .wrapper {
      display: flex;
      width: 100%;
    }

    .modal {
      width: 30vw;
      left: 35%;
    }
  }

  .header {
    display: flex;
    font-size: 10px;
    color: white;
    justify-content: space-between;
    padding: 0 10px;
    align-items: center;
    background-color: deepskyblue;

    i {
      cursor: pointer;
    }
  }

  .modal-content {
    ul {
      list-style: none;
    }
  }
</style>
