<template>
  <q-page class="flex flex-center">
    <div id="dropin-container"></div>
    <button id="submit-button">Request payment method</button>

  </q-page>
</template>

<script>
import {defineComponent} from 'vue';
import dropin from "braintree-web-drop-in";

export default defineComponent({
  name: 'PageIndex',
  created() {
    console.debug("crestde")
    const button = document.querySelector('#submit-button');
    debugger
    this.$api.post('/api/cart/products/payments/get-token/', {}, {
      headers: {
        Authorization: "Token"
      }
    })
      .then(({data}) => {
        console.debug('$api res data', data)
        return dropin.create({
          authorization: data.token,
          container: '#dropin-container'
        })
      }).then(instance => {
        debugger
        button.addEventListener('click', function () {
          instance.requestPaymentMethod(function (requestPaymentMethodErr, payload) {
            console.debug('payload')
          });
      });
    })
      .catch(err => {
        console.debug('$api err', err)
      })
  }
})
</script>
<!--<script>-->
<!--const startPaymentButton = document.querySelector('#start-payment-button');-->
<!--      var button = document.querySelector('#submit-button');-->


<!--      startPaymentButton.addEventListener('click', function () {-->

<!--      axios-->
<!--        .post('/api/v1/orders/39/pay-client-token/', {}, {-->
<!--        headers: {-->
<!--          Authorization: "Token 796aff865a47f2b479707b6b40c7299061055b6e"-->
<!--          }-->
<!--        })-->
<!--        .then(response => {-->
<!--        console.log('response from api')-->
<!--        console.log(response)-->
<!--        const token = response.data.token-->
<!--        braintree.dropin.create({-->
<!--            authorization: token,-->
<!--            container: '#dropin-container'-->
<!--            }, function (createErr, instance) {-->
<!--            button.addEventListener('click', function () {-->
<!--            instance.requestPaymentMethod(function (requestPaymentMethodErr, payload) {-->
<!--            // Submit payload.nonce to your server-->
<!--              });-->
<!--            });-->
<!--          });-->
<!--        });-->
<!--      })-->
<!--</script>-->
