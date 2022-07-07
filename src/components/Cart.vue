<script> 
    export default {
        data(){
            return {
                deliveryAddress: '',
                cartItems: [
                    {
                        id:1,
                        productDescription: 'Apple In-wired ear phone',
                        price: 1699,
                        originalPrice: 1900,
                        discount: 201,
                        quantity: 1,
                        productImg:'../../src/assets/wired.jpeg',
                        checked: true
                    },
                    {
                        id:2,
                        productDescription: 'Apple Earpods 1st generation',
                        price: 12999,
                        originalPrice: 18000,
                        discount: 5001,
                        quantity: 1,
                        productImg:'../../src/assets/secondGen.jpg',
                        checked: true
                    },
                    {
                        id:1,
                        productDescription: 'Apple Earpods Pro 1st generation',
                        price: 21999,
                        originalPrice: 23000,
                        discount: 1001,
                        quantity: 1,
                        productImg:'../../src/assets/airpodsPro.jpg',
                        checked: true
                    }
                ],
                cartTotal: 26597
            }
        },
        methods:{
            checkout(){
                const route ='Redirect';
                console.log('route', route);
            }
        },
        computed:{
            checkedCart(){
                return this.cartItems.filter((item)=> item.checked);
            },
            calculateCartValue(){
                return this.checkedCart.reduce((prev, curr)=>{
                    prev += (curr.quantity * curr.price);
                    return prev;
                }, 0)
            }
        },
        mounted(){
            console.log('This is the cart page')
        }
    }
</script>

<template>

    <section class="shopping-cart">

        <div class="shopping-cart__sections">
            <h2 class="shopping-cart__sections--title">Shopping Cart</h2>
            <a>Deselect all items</a>
        </div>
        <div v-if="checkedCart.length === 0" class="shopping-cart__sections">
            <strong class="shopping-cart__sections--empty-cart">No items added.</strong>
        </div>

        <div v-else class="shopping-cart__sections">
            <ul class="shopping-cart__items">
                        <li class="shopping-cart__items__line" v-for="item in checkedCart" :key="item.id">
                            <div class="shopping-cart__items__line-checkbox">
                                <input class="" type="checkbox" v-model="item.checked" id="{{item.id}}">
                            </div>
                            <div>
                                <picture>
                                    <img :src='item.productImg' :alt='item.productDescription' style='width: 100px;height: 100px;'/>
                                </picture>

                            </div>
                            <div class="shopping-cart__items__line--description">
                                {{item.productDescription}}
                                {{item.quantity}}
                            </div>
                            <div class="shopping-cart__items__line--quantity">
                                <select v-model="item.quantity">
                                    <option value='1'>1</option>
                                    <option value="2">2</option>
                                    <option value="3">3</option>
                                    <option value="4">4</option>
                                    <option value="5">5</option>
                                </select>
                            </div>
                            <div class="shopping-cart__items__line--price">
                                <div>Rs.{{item.price * item.quantity}}</div>
                            </div>
                        </li>
                    </ul>
            <div class="shopping-cart__total-amt">
                Subtotal : Rs.{{calculateCartValue}}
            </div>
        </div>
        
    </section>

</template>


<style>
    .shopping-cart{
        width: 100%;
        display: flex;
        flex-direction: column;
        place-items: center;
    }

    .shopping-cart__sections--title{
        font-size: 3rem;
        font-weight: bold;
    }

    .shopping-cart__title-sections, .shopping-cart__sections{
        width: 100%;
    }

    .shopping-cart__sections--empty-cart{
        font-size: 3rem;
        font-weight: 1000;
        margin: auto;
    }   
    .shopping-cart__items{
        list-style-type: none;
        width: 100%;
        margin: 0;
        padding: 1rem 2rem;
    }

    .shopping-cart__items__line{
        width: 100%;
        display: flex;
        justify-content: space-between;
        box-shadow: rgba(27, 31, 35, 0.04) 0px 1px 0px, rgba(255, 255, 255, 0.25) 0px 1px 0px inset;
        padding: 1.6rem 0;
    }

    .shopping-cart__items__line--description{
        min-width: 39.99rem;
        max-width: 40rem;
        padding: 0rem 1.6rem;
        font-size: 2rem;
    }

    .shopping-cart__items__line-checkbox{
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 0 1.6rem;
        padding-left: 3rem;
    }

    .shopping-cart__items__line--quantity{
        margin: 0 auto;
    }

    .shopping-cart__total-amt{
        width: 100%;
        display: flex;
        justify-content: flex-end;
        padding: 1rem 2rem;
        font-size: 2rem;
        font-weight: 1000;
    }

    .shopping-cart__items__line--price{
        min-width: 11.99rem;
        max-width: 12rem;
        text-align: right;
        font-size: 2rem;
        font-weight: 1000;
    } 
</style>