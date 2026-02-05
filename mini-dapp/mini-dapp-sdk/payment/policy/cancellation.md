---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/mini-dapp/mini-dapp-sdk/payment/policy/cancellation
---

# Cancellation

#### STRIPE

* Case.1 :  In the case where create API is hosted but SDK's startPayment has not been excuted
  * Max time for cancellation : 2100sec + 180sec
  * Response if payment is excuted after cancellation : Error when hosting SDK's startPayment
* Case.2 : SDK's startPayment is excuted but users don't approve on STRIPE page
  * Max time for cancellation : 400sec + 180sec
  * Response if payment is excuted after cancellation : Cannot payment excute with expiration

#### CRYPTO

* Case1. In the case whare creat API is hosted but SDK's startPayment has not been excuted
  * Max time for cancellation : 2100sec + 180sec
  * Response if payment is excuted after cancellation : Error when hosting SDK' startPayment
* Case2. SDK's startPayment is excuted but users don't approve transaction
  * Max time for cancellation : 100sec + 180sec
  * Response if payment is excuted after cancellation : Transaction failed with paying gas fee if approved
* Case3. SDK's startPayment is excuted and user approved transaction over max time for cancellation
  * Max time for cancellation : 100sec + 180sec
  * Response if payment is excuted after cancellation : Transaction failed with paying gas
