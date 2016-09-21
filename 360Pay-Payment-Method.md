# 360Pay Payment Method

## <abbr title="World Wide Web Consortium">W3C</abbr> Working Draft <time property="dcterms:issued" datetime="2016-09-18">18 September 2016</time>

<dl>

<dt>This version:</dt>

<dd></dd>

<dt>Latest published version:</dt>

<dd></dd>

<dt>Latest editor's draft:</dt>

<dd></dd>

<dt>Editors:</dt>

<dd property="bibo:editor" resource="_:editor0">Songfeng Li, Qihoo 360</dd>

<dd resource="_:editor1">Liangang Li, Qihoo 360</dd>

<dd resource="_:editor2">Chengyin Li, Qhioo 360</dd>


</dl>

[Copyright](http://www.w3.org/Consortium/Legal/ipr-notice#Copyright) © 2016 [<abbr title="World Wide Web Consortium">W3C</abbr>](http://www.w3.org/)<sup>®</sup> ([<abbr title="Massachusetts Institute of Technology">MIT</abbr>](http://www.csail.mit.edu/), [<abbr title="European Research Consortium for Informatics and Mathematics">ERCIM</abbr>](http://www.ercim.eu/), [Keio](http://www.keio.ac.jp/), [Beihang](http://ev.buaa.edu.cn/)). <abbr title="World Wide Web Consortium">W3C</abbr> [liability](http://www.w3.org/Consortium/Legal/ipr-notice#Legal_Disclaimer), [trademark](http://www.w3.org/Consortium/Legal/ipr-notice#W3C_Trademarks) and [permissive document license](http://www.w3.org/Consortium/Legal/2015/copyright-software-and-document) rules apply.

* * *

## Abstract

The 360Pay Payment Method specification describes the data formats used by the PaymentRequest API [<cite>[PAYMENTREQUESTAPI](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#bib-PAYMENTREQUESTAPI)</cite>] to support payment by 360pay.

## Status of This Document

_This section describes the status of this document at the time of its publication. Other documents may supersede this document. A list of current <abbr title="World Wide Web Consortium">W3C</abbr> publications and the latest revision of this technical report can be found in the [<abbr title="World Wide Web Consortium">W3C</abbr> technical reports index](https://www.w3.org/TR/) at https://www.w3.org/TR/._

This document was published by the [Web Payments Working Group](https://www.w3.org/Payments/WG/) as a Working Draft. If you wish to make comments regarding this document, please send them to [public-payments-wg@w3.org](mailto:public-payments-wg@w3.org)([subscribe](mailto:public-payments-wg-request@w3.org?subject=subscribe), [archives](https://lists.w3.org/Archives/Public/public-payments-wg/)). All comments are welcome.

Publication as a Working Draft does not imply endorsement by the <abbr title="World Wide Web Consortium">W3C</abbr> Membership. This is a draft document and may be updated, replaced or obsoleted by other documents at any time. It is inappropriate to cite this document as other than work in progress.

This document was produced by a group operating under the [5 February 2004 <abbr title="World Wide Web Consortium">W3C</abbr> Patent Policy](https://www.w3.org/Consortium/Patent-Policy-20040205/). The group does not expect this document to become a <abbr title="World Wide Web Consortium">W3C</abbr> Recommendation. <abbr title="World Wide Web Consortium">W3C</abbr> maintains a [public list of any patent disclosures](https://www.w3.org/2004/01/pp-impl/83744/status) made in connection with the deliverables of the group; that page also includes instructions for disclosing a patent. An individual who has actual knowledge of a patent which the individual believes contains [Essential Claim(s)](https://www.w3.org/Consortium/Patent-Policy-20040205/#def-essential) must disclose the information in accordance with[section 6 of the <abbr title="World Wide Web Consortium">W3C</abbr> Patent Policy](https://www.w3.org/Consortium/Patent-Policy-20040205/#sec-Disclosure).

This document is governed by the [1 September 2015 <abbr title="World Wide Web Consortium">W3C</abbr> Process Document](https://www.w3.org/2015/Process-20150901/).

<nav id="toc">

## table of contents

*   [1.Introduction](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#introduction)
*   [2.Dependencies](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#dependencies)
*   [3.Payment Method Identifier](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#method-id)
*   [4.Payment Method Specific Data for the PaymentRequest constructor](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#init-data)
*   [5.Payment Method Response](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#response)
*   [A.References](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#references)
    *   [A.1Normative references](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#normative-references)

</nav>

## 1. Introduction

_This section is non-normative._

This specification is a [Payment Method Specification](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#dfn-payment-transaction-message-specification) used by the Payment Request API [<cite>[PAYMENTREQUESTAPI](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#bib-PAYMENTREQUESTAPI)</cite>] to support payment by 360Pay. It is intended to provide compatibility for merchants who want to use 360Pay to ease adoption of the Payment Request API.

In the future, merchants should favor payment methods that provide a tokenized response rather than clear text credit card details.

## 2. Dependencies

This specification relies on several other underlying specifications.

<dl>

<dt>Payment Request API Architecture</dt>

<dd>The terms <dfn data-dfn-type="dfn" id="dfn-payment-method">Payment Method</dfn>, <dfn data-dfn-type="dfn" id="dfn-payment-app">Payment App</dfn>, and <dfn data-dfn-type="dfn" id="dfn-payment-transaction-message-specification">Payment Transaction Message Specification</dfn> are defined by the Payment Request Architecture document [<cite>[PAYMENTARCH](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#bib-PAYMENTARCH)</cite>].</dd>

<dt>Payment Request API</dt>

<dd>The term <dfn data-dfn-type="dfn" id="dfn-paymentrequest-constructor">PaymentRequest constructor</dfn> is defined by the PaymentRequest API specification [<cite>[PAYMENTREQUESTAPI](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#bib-PAYMENTREQUESTAPI)</cite>].</dd>

<dt>Payment Method Identifiers</dt>

<dd>The term <dfn data-dfn-type="dfn" id="dfn-payment-method-identifier">Payment Method Identifier</dfn> is defined by the Payment Method Identifiers specification [<cite>[METHODIDENTIFIERS](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#bib-METHODIDENTIFIERS)</cite>].</dd>

<dt>Web IDL</dt>

<dd>The IDL in this specification is defined by Web IDL [<cite>[WEBIDL](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#bib-WEBIDL)</cite>].</dd>

</dl>

## 3. Payment Method Identifier

The following [payment method identifier](https://w3c.github.io/webpayments/proposals/360pay-payment-method.html#dfn-payment-method-identifier) strings are supported by the 360pay Payment data formats.

| Identifier String | Description |
| 360pay | 360Pay |


## 4. Payment Method Specific Data for the PaymentRequest constructor

This section describes payment method specific data that is supplied as part of the `methodData` argument to the PaymentRequest constructor.

The payment method specific data used by the PaymentRequest constructor when processing 360Pay Payment method is as following.

### 4.1 Payment Method Specific Data

```
dictionary [`PaymentMethodSpecificData`]{
 required DOMString       mer_code;
 required DOMString       mer_trade_code;
 required DOMString       trans_service;
 required DOMString       input_cha;
 required DOMString       sign_type;
 required DOMString       sign;
 required DOMString       notify_url;
 required DOMString       return_url;
 required DOMString       rec_amount; 
 required DOMString       product_name;   
 		  DOMString       product_price; 	
 		  DOMString       pay_type;	 
 		  DOMString       qr_pay_mode;
 		  DOMString       md_time;
 		  DOMString       mer_order_time; 		  
 		  DOMString       timeout_set; 		
 		  DOMString       bank_code; 		  
};
```


The `PaymentMethodSpecificData` dictionary contains the following fields:

<dl>

<dt><dfn data-dfn-type="dfn" id="dfn-mercode">`mer_code`</dfn></dt>

<dd>The `mer_code` field contains the merchant's ID assigned by 360Pay.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-mertradecode">`mer_trade_code`</dfn></dt>

<dd>The `mer_trade_code` field contains the merchant's order number.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-transservice">`trans_service`</dfn></dt>

<dd>The `trans_service` field contains the service type selected by the merchant while sending the request.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-inputcha">`input_cha`</dfn></dt>

<dd>The `input_cha` field contains the character encoding type of the merchant's website.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-signtype">`sign_type`</dfn></dt>

<dd>The `sign_type` field contains the signature type.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-sign">`sign`</dfn></dt>

<dd>The `sign` field contains the signature content.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-notifyurl">`notify_url`</dfn></dt>

<dd>The `notify_url` field contains the URL that will used by the asynchronous notification.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-returnurl">`return_url`</dfn></dt>

<dd>The `return_url` field contains the URL that will used by synchronous notification.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-recamount">`rec_amount`</dfn></dt>

<dd>The `rec_amount` field contains the total amount of the order.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-productname">`product_name`</dfn></dt>

<dd>The `product_name` field contains the product's name.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-productprice">`product_price`</dfn></dt>

<dd>The `product_price` field contains the product's price.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-paytype">`pay_type`</dfn></dt>

<dd>The `pay_type` field contains the payment type.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-qrpaymode">`qr_pay_mode`</dfn></dt>

<dd>The `qr_pay_mode` field contains number 1 or 0, mean seperately to generate the qrcode and not to genertate the qrcode.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-mdtime">`md_time`</dfn></dt>

<dd>The `md_time` field contains the anti-fishing attack timestamp.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-merordertime">`mer_order_time`</dfn></dt>

<dd>The `mer_order_time` field contains the merchant's order time.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-timeoutset">`timeout_set`</dfn></dt>

<dd>The `timeout_set` field contains the timeout value in milliseconds for the asynchronous notification.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-bankcode">`bank_code`</dfn></dt>

<dd>The `bank_code` field contains the bank code.</dd>

</dl>


## 5. Payment Method Response

The `PaymentMethodResponse` dictionary contains the response from the Payment Request API when an user accepts payment with 360Pay.

### 5.1 PaymentMethodResponse

```
dictionary [`PaymentMethodResponse`]{
 required DOMString       gateway_trade_code;
 required DOMString       inner_trade_code;
 required DOMString       sign; 
		  DOMString       bank_code;
		  DOMString       pay_time;
		  DOMString       bank_pay_flag;
		  DOMString       bank_trade_code;
		  DOMString       mer_code;		
		  DOMString       mer_trade_code;		
		  DOMString       input_cha;		
		  DOMString       sign_type;		
		  DOMString       product_name;			
		  DOMString       rec_amount;		
		  DOMString       pay_amount;
		  DOMString       md_time;		
		  DOMString       product_price;		
};
```

The `PaymentMethodResponse` dictionary contains the following fields:

<dl>

<dt><dfn data-dfn-type="dfn" id="dfn-gatewaytradecode">`gateway_trade_code`</dfn></dt>

<dd>The `gateway_trade_code` field contains the gateway trade code.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-innertradecode">`inner_trade_code`</dfn></dt>

<dd>The `inner_trade_code` field contains the inner trade code.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-sign">`sign`</dfn></dt>

<dd>The `sign` field contains the signature content.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-bankcode">`bank_code`</dfn></dt>

<dd>The `bank_code` field contains the bank code.</dd>


<dt><dfn data-dfn-type="dfn" id="dfn-paytime">`pay_time`</dfn></dt>

<dd>The `pay_time` field contains the payment time, if not empty, the format is 'YYYYMMDDHHMMSS'.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-bankpayflag">`bank_pay_flag`</dfn></dt>

<dd>The `bank_pay_flag` field contains the payment result, 'success' mean the payment has completed successfully, 'fail' mean the payment has failed, and '' mean the payment process has unexpectedly interrupted.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-banktradecode">`bank_trade_code`</dfn></dt>

<dd>The `bank_trade_code` field contains the bank trade code</dd>


<dt><dfn data-dfn-type="dfn" id="dfn-mercode">`mer_code`</dfn></dt>

<dd>The `mer_code` field contains the merchant's ID assigned by 360Pay.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-mertradecode">`mer_trade_code`</dfn></dt>

<dd>The `mer_trade_code` field contains the merchant's order number.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-inputcha">`input_cha`</dfn></dt>

<dd>The `input_cha` field contains the character encoding type of the merchant's website.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-signtype">`sign_type`</dfn></dt>

<dd>The `sign_type` field contains the signature type.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-productname">`product_name`</dfn></dt>

<dd>The `product_name` field contains the product name.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-recamount">`rec_amount`</dfn></dt>

<dd>The `rec_amount` field contains the total amount of the order.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-payamount">`pay_amount`</dfn></dt>

<dd>The `pay_amount` field contains the actual amount of the payment.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-mdtime">`md_time`</dfn></dt>

<dd>The `md_time` field contains the anti-fishing attack timestamp.</dd>

<dt><dfn data-dfn-type="dfn" id="dfn-productprice">`product_price`</dfn></dt>

<dd>The `product_price` field contains the product price.</dd>


</dl>


## A. References

### A.1 Normative references

<dl resource="">

<dt id="bib-METHODIDENTIFIERS">[METHODIDENTIFIERS]</dt>

<dd>Adrian Bateman; Zach Koch; Richard Barnes; Roy McElmurry. [<cite>Payment Method Identifiers</cite>](https://www.w3.org/TR/payment-method-id/). W3C Working Draft. URL: [https://www.w3.org/TR/payment-method-id/](https://www.w3.org/TR/payment-method-id/)</dd>

<dt id="bib-PAYMENTARCH">[PAYMENTARCH]</dt>

<dd>Adrian Bateman; Zach Koch; Richard Barnes; Roy McElmurry. [<cite>Payment Request Architecture</cite>](https://w3c.github.io/browser-payment-api/specs/architecture.html). W3C Editor's Draft. URL: [https://w3c.github.io/browser-payment-api/specs/architecture.html](https://w3c.github.io/browser-payment-api/specs/architecture.html)</dd>

<dt id="bib-PAYMENTREQUESTAPI">[PAYMENTREQUESTAPI]</dt>

<dd>Adrian Bateman; Zach Koch; Richard Barnes; Roy McElmurry. [<cite>Payment Request API</cite>](https://www.w3.org/TR/payment-request/). W3C Working Draft. URL: [https://www.w3.org/TR/payment-request/](https://www.w3.org/TR/payment-request/)</dd>

<dt id="bib-WEBIDL">[WEBIDL]</dt>

<dd>Cameron McCormack; Boris Zbarsky. W3C. [<cite>WebIDL Level 1</cite>](http://www.w3.org/TR/WebIDL-1/). 8 March 2016\. W3C Candidate Recommendation. URL: [http://www.w3.org/TR/WebIDL-1/](http://www.w3.org/TR/WebIDL-1/)</dd>

</dl>
