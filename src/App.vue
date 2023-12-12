<template>
<div class="wrapper">
        <div class="row" v-if="products.length">  <!--This allows you to check if the condition is true or if something is inside the array and it will display the elements if true. If false, it will display the spinner-->
          <!-- v-if removes the respective element from the dom -->
          <!-- v-show would be the same as display:none so the element will be hidden -->

            <div class="prodCard" v-for="product in products" :key="product.id">
              <!-- Dont apply if statement and for loop on one line. Use the parent element for the if statement and the child statement for the loop -->
              <!-- When using a for loop, you need to make sure that each card is unique so you need to bind the key to the id (:key="product.id") -->
                <div class="card-header">
                    <h3>{{ product.prodName }}</h3> 
                    <!-- use a double moustache / v-text="" -->
                </div>

                <div class="card-body">
                    <img :src="product.image" :alt="product.prodName" loading="lazy" @mouseenter="onMouseEnter" @mouseleave="onMouseLeave">
                    <!-- Use v-bind /:src when assigning a variable value to an attribute. In this case we are using the properties of the product object -->

                    <p :class="product.amount > 420 ? 'expensive' : 'cheap'">R{{ product.amount.toFixed(2) }}</p>
                    <!-- If the cost is more than R420 then you need to apply a certain class.  -->
                    <!-- use turnary operator to check if the product cost is more than R420 -->
                    <!-- you need to bind the attribute if the attribue value is a variable name -->
                    <!-- :class = "{expensive : product.amount > 420}" -->

                </div>
                <div class="card-footer">
                    <a href="#" type="button">View Details</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
        name: 'App',
        data() { //factory function because it creates and returns an object. Data is called a reactive state. This is where you declare variables using the options api
            return {
                products: [
                    {
                        id: 1,
                        prodName: 'Python Crash Course',
                        category: 'Python',
                        amount: 400.9999,
                        image: 'https://i.postimg.cc/MKDLBPYm/Python-Crash-Course-cover.jpg'
                    },
                    {
                        id: 2,
                        prodName: 'Python Programming',
                        category: 'Python',
                        amount: 900.4586,
                        image: 'https://i.postimg.cc/rFcbKX5p/Python-Programming-for-Beginners-cover.jpg'
                    },
                    {
                        id: 3,
                        prodName: 'Mastering C++',
                        category: 'C++',
                        amount: 1800.896,
                        image: 'https://i.postimg.cc/Ss9zrpfT/Mastering-C-Programming.jpg'
                    },
                ]
            }
        },
        computed() {},
        methods: {
            onMouseEnter() {
                alert('Hello there')
            },
            onMouseLeave() {
                alert('Bye')
            }
        }
    }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.wrapper :is(.row) {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.prodCard {
  width: 18rem;
}
.prodCard :is(>*, img){
  width: 100%;
  aspect-ratio: 1/1;
}
.expensive {
  font-weight: bolder;
  color: darkkhaki;
}
.cheap {
  color: black;
}
</style>
