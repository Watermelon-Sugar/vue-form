<template>
  <form @submit.prevent="placeOrder">
      <label>Name</label>
      <input type="text" required v-model="name">
        <div v-if="nameError" class="name-error">{{nameError}} </div>
      
      <label>Email</label>
      <input type="email" required v-model="email">

      
      <label>Shoe Size</label>
      <input type="text" required v-model="size">

      
      <label>Preferred Shoe Type</label>
      <select v-model="type">
        <option value="Oxfords">Oxfords</option>
        <option value="Derby">Derby</option>
        <option value="Chelsea Boots">Chelsea Boots</option>
        <option value="Combant Boots">Combant Boots</option>
        <option value="Sandals">Sandals</option>
        <option value="Slides">Slides</option>
        <option value="Mules">Mules</option>
      </select>

        <label>Delivery Mode</label>
        <input type="text" v-model="delivery" @keyup.alt="details"> 

        <div v-for="mode in deliveryMode" :key="mode" class="md">
           <span @click="deleteDetails(mode)"> {{mode}} </span>
        </div>

      <div class="choice">
        <input type="checkbox" v-model="choice" required>
        <label>Choices Confirmed</label>
      </div>

        <div class="submit">
            <button>Place Your Order</button>
        </div>


      <!-- <div>
        <input type="checkbox" value="Asgard" v-model="names">
        <label>Asgard</label>
      </div>

      <div>
        <input type="checkbox" value="Ymir" v-model="names">
        <label>Ymir</label>
      </div>
      
      <div>
        <input type="checkbox" value="Ragnar" v-model="names">
        <label>Ragnar</label>
      </div> -->

    </form>

  

    <!-- <p>Name: {{name}}</p>
    <p>Email: {{email}}</p>
    <p>Shoe Size: {{size}}</p>
    <p>Preferred Shoe Type: {{type}}</p>
    <p>Choice: {{choice}}</p>
    <p>Names: {{names}} </p> -->
</template>

<script>
export default {
    data() {
        return {
            email: '',
            name: '',
            size: '',
            type: 'Oxfords',
            choice: false,
            delivery: '',
            deliveryMode: [],
            nameError: ''
            // names: []
        }
    },
    methods: {
        details(e) {
            if (e.key === '.' && this.delivery) {
                if (!this.deliveryMode.includes(this.delivery)) {
                this.deliveryMode.push(this.delivery)
                }

                this.delivery = ''
            }
        },
        deleteDetails(mode) {
            this.deliveryMode = this.deliveryMode.filter((item) => {
                return mode !== item
            })
        },
        placeOrder() {
            // validate name
            this.nameError = this.name.length > 2 ? '' : 'Name must be more than two characters!'

            if(!this.nameError) {
                console.log('name: ', this.name)
                console.log('email: ', this.email)
                console.log('shoe size: ', this.size)
                console.log('shoe type: ', this.type)
                console.log('delivery mode: ', this.delivery)
                console.log('choice: ', this.choice)
            }
        }
    }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 10px auto;
        background: rgb(226, 162, 66);
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }

    label {
        color: #efefef;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.7rem;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }

    input, select {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;       
        border-radius: 8px;
        color: #555;
    }

    input:focus, select:focus {
        outline: none;
    }

    input[type="checkbox"] {
        display: inline-block;
        width: 15px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }

    .md {
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #ccc;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #651;
        cursor: pointer;
    }

    .submit {
        text-align: center;
    }

    button {
        background: #fcc;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: #555;
        border-radius: 20px;
        cursor: pointer;
    }

    .name-error {
        color: red;
        margin-top: 10px;
        font-size: 0.8rem;
        font-weight: bold;
    }

</style>