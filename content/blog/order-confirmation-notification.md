---
author: Driss Oudmine
title: How to add a custom Shopify Notification Email template - Order Confirmation
description: Learn how to add a custom email Order confirmation template to your Shopify store
date: 2022-06-21
thumbnail: /order-confirmation.png
draft: true
---

In this tutorial we will be replacing the default email Order confirmation template with a custom one that is modern and unique. Also you will be able to add your logo, colors and images plus a discount code! All this without the need of an app. So let's get started

1. Go to **Settings** > **Notifications** then click on _Order confirmation_ under _Orders_ section
2. Copy and paste the following code inside Email body (HTML):
```html {linenos=table}
{% assign banner_image = "http://placehold.jp/600x427.png" %}
{% assign discount_image = "http://placehold.jp/1181x1280.png" %}
{% assign amount_off = "$10 OFF" %}
{% assign discount_code = "DISCOUNT10" %}

{% capture email_title %}
  Thanks for your purchase!
{% endcapture %}

{% capture hero_title %}
  <strong style="box-sizing: border-box;">Thanks for your</strong><br>
  <strong style="box-sizing: border-box;">purchase!</strong>
{% endcapture %}

{% capture hero_description %}
  {% if requires_shipping %}
    {% case delivery_method %}
      {% when 'pick-up' %}
        You’ll receive an email when your order is ready for pickup.
      {% when 'local' %}
        Hi {{ customer.first_name }}, we're getting your order ready for delivery.
      {% else %}
        Hi {{ customer.first_name }}, we're getting your order ready to be shipped. We will notify you when it has been
        sent.
    {% endcase %}
    {% if delivery_instructions != blank %}
      <p>
        <b>Delivery information:</b>
        {{ delivery_instructions }}
      </p>
    {% endif %}
    {% if consolidated_estimated_delivery_time %}
      <p>
        Estimated delivery
        <b>{{ consolidated_estimated_delivery_time }}</b>
      </p>
    {% endif %}
  {% endif %}
{% endcapture %}

<!doctype html>
<html style="box-sizing: border-box;">
  <head style="box-sizing: border-box;">
    <meta charset="utf-8" style="box-sizing: border-box;">
    <meta name="viewport" content="width=device-width" style="box-sizing: border-box;">
    <meta http-equiv="X-UA-Compatible" content="IE=edge" style="box-sizing: border-box;">
    <meta name="x-apple-disable-message-reformatting" style="box-sizing: border-box;">
    <title style="box-sizing: border-box;"></title>
    <style style="box-sizing: border-box;">
      @media all {
        .ExternalClass,
        .ExternalClass p,
        .ExternalClass span,
        .ExternalClass font,
        .ExternalClass td,
        .ExternalClass div {
          line-height: 100%;
        }
        .apple-link a {
          color: inherit !important;
          font-family: inherit !important;
          font-size: inherit !important;
          font-weight: inherit !important;
          line-height: inherit !important;
          text-decoration-line: none !important;
          text-decoration-thickness: initial !important;
          text-decoration-style: initial !important;
          text-decoration-color: initial !important;
        }
        #MessageViewBody a {
          color: inherit;
          text-decoration-line: none;
          text-decoration-thickness: initial;
          text-decoration-style: initial;
          text-decoration-color: initial;
          font-size: inherit;
          font-family: inherit;
          font-weight: inherit;
          line-height: inherit;
        }
        .btn-primary table td:hover {
          background-color: rgb(52, 73, 94) !important;
        }
        .btn-primary a:hover {
          background-color: rgb(52, 73, 94) !important;
          border-top-color: rgb(52, 73, 94) !important;
          border-right-color: rgb(52, 73, 94) !important;
          border-bottom-color: rgb(52, 73, 94) !important;
          border-left-color: rgb(52, 73, 94) !important;
        }
      }
      @media only screen and (min-width: 768px) {
        .mobile-only table,
        .mobile-only td {
          padding-top: 0px !important;
          padding-bottom: 0px !important;
          padding-left: 0px !important;
          padding-right: 0px !important;
          padding: 0px !important;
          mso-padding-alt: 0px 0px 0px 0px !important;
        }
      }
      @media (max-width: 767px) {
        .mb-center {
          text-align: center !important;
        }
        .pr-0 {
          padding-right: 0px !important;
        }
        .pl-0 {
          padding-left: 0px !important;
        }
        .row-wrap>td {
          display: table !important;
          width: 100% !important;
        }
        .desktop-only table,
        .desktop-only td,
        .desktop-only tr,
        .desktop-only th {
          display: none !important;
        }
        .mobile-only table {
          display: table !important;
        }
        .mobile-only td {
          display: table-cell !important;
        }
        .mobile-only tr {
          display: table-row !important;
        }
        .mobile-only .button-container td a {
          display: block;
          padding: 10px 60px;
        }
        .mobile-only .divider-padding {
          padding: 15px 0px;
          mso-padding-alt: 15px 0px;
        }
        .mobile-only td.divider-line-2 {
          font-size: 2px;
          height: 2px;
          line-height: 2px;
        }
        .mobile-only .coupon-container td {
          padding: 10px 0px !important;
          mso-padding-alt: 10px 0px !important;
        }
        .mobile-only .coupon-container {
          border-width: 3px;
          border-style: dashed;
        }
        .mobile-only tr.row-hidden {
          display: none !important;
        }
      }
      @media only screen and (max-width: 699px) {
        table.table-640,
        div.row {
          width: 100% !important;
          max-width: 100% !important;
        }
        img.mo-img-full {
          width: 100% !important;
        }
        td.mo-text-center {
          text-align: center !important;
        }
        table.mo-link td {
          width: 100% !important;
          display: block !important;
          text-align: center !important;
        }
        table.mo-link td a,
        td.mo-link a {
          display: block !important;
          text-align: center !important;
          padding-bottom: 15px !important;
          border-bottom-width: 2px !important;
          border-bottom-style: solid !important;
          border-bottom-color: rgb(241, 241, 241) !important;
        }
      }
      @media only screen and (max-width: 620px) {
        table[class="body"] h1 {
          font-size: 28px !important;
          margin-bottom: 10px !important;
        }
        table[class="body"] p,
        table[class="body"] ul,
        table[class="body"] ol,
        table[class="body"] td,
        table[class="body"] span,
        table[class="body"] a {
          font-size: 16px !important;
        }
        table[class="body"] .wrapper,
        table[class="body"] .article {
          padding-top: 10px !important;
          padding-right: 10px !important;
          padding-bottom: 10px !important;
          padding-left: 10px !important;
        }
        table[class="body"] .content {
          padding-top: 0px !important;
          padding-right: 0px !important;
          padding-bottom: 0px !important;
          padding-left: 0px !important;
        }
        table[class="body"] .container {
          padding-top: 0px !important;
          padding-right: 0px !important;
          padding-bottom: 0px !important;
          padding-left: 0px !important;
          width: 100% !important;
        }
        table[class="body"] .main {
          border-left-width: 0px !important;
          border-top-left-radius: 0px !important;
          border-top-right-radius: 0px !important;
          border-bottom-right-radius: 0px !important;
          border-bottom-left-radius: 0px !important;
          border-right-width: 0px !important;
        }
        table[class="body"] .btn table {
          width: 100% !important;
        }
        table[class="body"] .btn a {
          width: 100% !important;
        }
        table[class="body"] .img-responsive {
          height: auto !important;
          max-width: 100% !important;
          width: auto !important;
        }
      }
      @media (max-width: 600px) {
        .row-wrap>td {
          display: table !important;
          width: 100% !important;
        }
      }
    </style>
  </head>

  <body class="" style="box-sizing: border-box; margin: 0;">
    <body style="background-color: undefined; box-sizing: border-box; margin: 0;">
      <meta charset="utf-8" style="box-sizing: border-box;">
      <meta name="viewport" content="width=device-width" style="box-sizing: border-box;">
      <meta http-equiv="X-UA-Compatible" content="IE=edge" style="box-sizing: border-box;">
      <meta name="x-apple-disable-message-reformatting" style="box-sizing: border-box;">
      <title style="box-sizing: border-box;"></title>
      <link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,600,700" rel="stylesheet" style="box-sizing: border-box;">
      <!--
        [if(mso)|(mso 16)]>
        <style type="text/css">
        a {text-decoration: none;}
        </style>
        <![endif]
      -->
      <center bgcolor="#ffffff" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; background: #ffffff; background-image: none; box-sizing: border-box; color: rgba(0,0,0,.4); font-family: 'Roboto', sans-serif; font-size: 16px; font-weight: 400; line-height: 1.8; margin: 0 auto; mso-line-height-rule: exactly; padding: 50px 0px; padding-top: 0px; width: 100%;">
        <table cellpadding="0" align="center" width="100%" bgcolor="#ffffff" class="wrapper-inner" style="background: #ffffff; border: 0; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; max-width: 100%; mso-padding-alt: 50px 0px; padding: 50px 0px;" border="0" cellspacing="0">
          <tbody style="box-sizing: border-box;">
            <tr style="box-sizing: border-box;">
              <td align="center" style="box-sizing: border-box;">
                <table cellpadding="0" align="center" width="600" bgcolor="#ffffffff" class="table-640" style="background: #FFFFFF; background-image: none; border: 0; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; max-width: 600px;" border="0" cellspacing="0">
                  <tbody bgcolor="#ffffffff" style="background-color: #FFFFFF; background-image: none; box-sizing: border-box;">
                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                      <td valign="middle" align="center" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 15px;">
                        <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                          <tbody style="box-sizing: border-box;">
                            <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                              <td valign="middle" align="center" class="logo" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                                <a href="{{ shop.url }}" target="_blank" style="box-sizing: border-box; max-width: 100%;">
                                  {%- if shop.email_logo_url %}
                                    <img width="{{ shop.email_logo_width }}" src="{{ shop.email_logo_url }}" alt="{{ shop.name }}" style="-ms-interpolation-mode: bicubic; box-sizing: border-box; display: block; height: auto; margin: auto; outline: none; text-decoration: none;">
                                  {%- else %}
                                    <h1 style="font-weight: normal; font-size: 30px; color: #333; margin: 0;">
                                      {{ shop.name }}
                                    </h1>
                                  {%- endif %}
                                </a>
                              </td>
                            </tr>
                          </tbody>
                        </table>
                      </td>
                    </tr>
                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                      <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                        <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                          <tbody style="box-sizing: border-box;">
                            <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                              <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                  <tbody style="box-sizing: border-box;">
                                    <tr class="row-wrap" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                      <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;" width="100%">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                              <td align="center" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                                                <a alt="" target="_blank" class="image-link-wrapper" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; display: block; height: auto; max-width: 100%; width: 100%;"><img src="{{ banner_image }}" align="top" width="600" height="auto" border="0" loading="lazy" style="box-sizing: border-box; height: auto; width: 100%;"></a>
                                              </td>
                                            </tr>
                                            <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                              <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                                                <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                                  <tbody style="box-sizing: border-box;">
                                                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                                      <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                                        <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                                          <tbody style="box-sizing: border-box;">
                                                            <tr class="row-wrap" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                                              <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;" width="100%">
                                                                <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                                                  <tbody style="box-sizing: border-box;">
                                                                    <tr style="box-sizing: border-box; color: #000;">
                                                                      <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 30px 10px 10px; padding-bottom: 10px; padding-left: 10px; padding-right: 10px; padding-top: 30px;">
                                                                        <div style="box-sizing: border-box; color: #000000; font-size: 16px; font-weight: 400; line-height: normal; text-align: center;">
                                                                          <p style="box-sizing: border-box; margin: 0;">
                                                                            <span style="box-sizing: border-box; color: #434343; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; font-size: 30px;">
                                                                              <strong style="box-sizing: border-box;">
                                                                                {{ hero_title }}
                                                                              </strong> </span><br style="box-sizing: border-box;">
                                                                          </p>
                                                                        </div>
                                                                      </td>
                                                                    </tr>
                                                                    <tr style="box-sizing: border-box; color: #000;">
                                                                      <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 10px 40px 10px 40px; padding-bottom: 10px; padding-left: 40px; padding-right: 40px; padding-top: 10px;">
                                                                        <div style="box-sizing: border-box; line-height: normal;">
                                                                          <p style="box-sizing: border-box; margin: 0; text-align: center;">
                                                                            <span style="box-sizing: border-box; color: #363636; font-size: 18px;">
                                                                              {{ hero_description }}
                                                                            </span>
                                                                          </p>
                                                                          <p style="box-sizing: border-box; margin: 0;">
                                                                            &nbsp;
                                                                          </p>
                                                                        </div>
                                                                      </td>
                                                                    </tr>
                                                                  </tbody>
                                                                </table>
                                                              </td>
                                                            </tr>
                                                          </tbody>
                                                        </table>
                                                      </td>
                                                    </tr>
                                                  </tbody>
                                                </table>
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                    </tr>
                                  </tbody>
                                </table>
                              </td>
                            </tr>
                          </tbody>
                        </table>
                      </td>
                    </tr>

                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; background: #f7f7f7; box-sizing: border-box;">
                      <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                        <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                          <tbody style="box-sizing: border-box;">
                            <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                              <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                  <tbody style="box-sizing: border-box;">
                                    <tr class="row-wrap" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                      <td valign="top" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 15px; padding-left: 15px; padding-right: 15px; padding-top: 5px;" width="33.33%" align="left">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="box-sizing: border-box; color: #000;">
                                              <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 15px 15px 0px 15px; padding: 15px 15px 0px 15px;">
                                                <h2 class="mb-center" style="margin: 0 0 12px 0; box-sizing: border-box; line-height: 1; text-align: left;">
                                                  <span style="box-sizing: border-box; color: #434343; font-size: 16px;">
                                                    Order number
                                                  </span>
                                                </h2>

                                                <p class="mb-center" style="color: {{ shop.email_accent_color }}; font-size: 16px; box-sizing: border-box; line-height: 1.2; margin: 0; text-align: left;">
                                                  <span>{{ order_name }}</span>
                                                </p>
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                      <td valign="top" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 15px; padding-left: 15px; padding-right: 15px; padding-top: 5px;" width="33.33%" align="left">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="box-sizing: border-box; color: #000;">
                                              <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 15px 15px 0px 15px; padding: 15px 15px 0px 15px;">
                                                <h2 class="mb-center" style="margin: 0 0 12px 0; box-sizing: border-box; line-height: 1; text-align: left;">
                                                  <span style="box-sizing: border-box; color: #434343; font-size: 16px;">
                                                    Order date
                                                  </span>
                                                </h2>
                                                <p class="mb-center" style="color: {{ shop.email_accent_color }}; font-size: 16px; box-sizing: border-box; line-height: 1.2; margin: 0; text-align: left;">
                                                  <span> {{ created_at | date: format: 'abbreviated_date' }}</span>
                                                </p>
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                      <td valign="top" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 15px; padding-left: 15px; padding-right: 15px; padding-top: 5px;" width="33.33%" align="left">
                                        <table valign="top" role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="box-sizing: border-box; color: #000;">
                                              <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 15px 15px 0px 15px; padding: 15px 15px 0px 15px;">
                                                <h2 class="mb-center" style="margin: 0 0 12px 0; box-sizing: border-box; line-height: 1; text-align: left;">
                                                  <span style="box-sizing: border-box; color: #434343; font-size: 16px;">
                                                    Shipping method
                                                  </span>
                                                </h2>

                                                {% if requires_shipping and shipping_address %}
                                                  <p class="mb-center" style="box-sizing: border-box; line-height: 1.5; margin: 0; text-align: justify; color: {{ shop.email_accent_color }}; font-size: 16px;">
                                                    <span>{{ shipping_method.title }}</span>
                                                  </p>
                                                {% endif %}
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                    </tr>
                                  </tbody>
                                </table>
                              </td>
                            </tr>
                          </tbody>
                        </table>
                      </td>
                    </tr>
                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; background: #f7f7f7; box-sizing: border-box;">
                      <td style="padding-top: 10px;-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                        <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                          <tbody style="box-sizing: border-box;">
                            <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                              <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                  <tbody style="box-sizing: border-box;">
                                    <tr class="row-wrap" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                      <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 15px; padding-left: 15px; padding-right: 15px; padding-top: 5px;" width="33.33%" align="left">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="box-sizing: border-box; color: #000;">
                                              <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 0px 10px 15px; padding-bottom: 10px; padding-left: 15px; padding-right: 0px; padding-top: 0px;">
                                                <h2 class="mb-center" style="margin: 0 0 12px 0; box-sizing: border-box; line-height: 1; text-align: left;">
                                                  <span style="box-sizing: border-box; color: #434343; font-size: 16px;">
                                                    Shipping address
                                                  </span>
                                                </h2>
                                                {% if requires_shipping %}
                                                  <p class="mb-center" style="color: {{ shop.email_accent_color }}; font-size: 16px; box-sizing: border-box; line-height: 1.2; margin: 0; text-align: left;">
                                                    {% if shipping_address.name %}
                                                      <span>{{ shipping_address.name }}</span><br style="box-sizing: border-box;">
                                                    {% endif %}
                                                    {% if shipping_address.street %}
                                                      <span>{{ shipping_address.street }}</span><br style="box-sizing: border-box;">
                                                    {% endif %}
                                                    {% if shipping_address.city %}
                                                      <span>{{ shipping_address.city }}</span><br style="box-sizing: border-box;">
                                                    {% endif %}
                                                    {% if shipping_address.province %}
                                                      <span>{{ shipping_address.province }}</span><br style="box-sizing: border-box;">
                                                    {% endif %}
                                                    {% if shipping_address.zip %}
                                                      <span>{{ shipping_address.zip }}</span><br style="box-sizing: border-box;">
                                                    {% endif %}
                                                    {% if shipping_address.country %}
                                                      <span>{{ shipping_address.country }}</span><br style="box-sizing: border-box;">
                                                    {% endif %}
                                                  </p>
                                                {% endif %}
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                      <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 15px; padding-left: 15px; padding-right: 15px; padding-top: 5px;" width="33.33%" align="left">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="box-sizing: border-box; color: #000;">
                                              <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 0px 10px 15px; padding-bottom: 10px; padding-left: 15px; padding-right: 0px; padding-top: 0px;">
                                                <h2 class="mb-center" style="margin: 0 0 12px 0; box-sizing: border-box; line-height: 1; text-align: left;">
                                                  <span style="box-sizing: border-box; color: #434343; font-size: 16px;">
                                                    Billing address
                                                  </span>
                                                </h2>
                                                <p class="mb-center" style="color: {{ shop.email_accent_color }}; font-size: 16px; box-sizing: border-box; line-height: 1.2; margin: 0; text-align: left;">
                                                  {% if billing_address.name %}
                                                    <span>{{ billing_address.name }}</span><br style="box-sizing: border-box;">
                                                  {% endif %}
                                                  {% if billing_address.street %}
                                                    <span>{{ billing_address.street }}</span><br style="box-sizing: border-box;">
                                                  {% endif %}
                                                  {% if billing_address.city %}
                                                    <span>{{ billing_address.city }}</span><br style="box-sizing: border-box;">
                                                  {% endif %}
                                                  {% if billing_address.province %}
                                                    <span>{{ billing_address.province }}</span><br style="box-sizing: border-box;">
                                                  {% endif %}
                                                  {% if billing_address.zip %}
                                                    <span>{{ billing_address.zip }}</span><br style="box-sizing: border-box;">
                                                  {% endif %}
                                                  {% if billing_address.country %}
                                                    <span>{{ billing_address.country }}</span><br style="box-sizing: border-box;">
                                                  {%- endif %}
                                                </p>
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                      <td valign="top" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 15px; padding-left: 15px; padding-right: 15px; padding-top: 5px;" width="33.33%" align="left">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="box-sizing: border-box; color: #000;">
                                              <td align="center" style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 0px 10px 15px; padding-bottom: 10px; padding-left: 15px; padding-right: 0px; padding-top: 0px;">
                                                <h2 class="mb-center" style="margin: 0 0 12px 0; box-sizing: border-box; line-height: 1; text-align: left;">
                                                  <span style="box-sizing: border-box; color: #434343; font-size: 16px;">
                                                    Payment method
                                                  </span>
                                                </h2>
                                                {% for transaction in transactions %}
                                                  {% if transaction.status == "success" or transaction.status == "pending" %}
                                                    {% if transaction.kind == "authorization" or transaction.kind == "sale" %}
                                                      {% if transaction.payment_details.credit_card_company %}
                                                        <table role="presentation" style="border-collapse:collapse;border:0;border-spacing:0;margin: 0; text-align: left; color: {{ shop.email_accent_color }}; font-size: 16px;">
                                                          <tr>
                                                            <td valign="top" style="padding:0;width:24px;">
                                                              <img src="{{ transaction.payment_details.credit_card_company | payment_icon_png_url }}" style="height: 24px;display: inline-block;" height="24" alt="{{ transaction.payment_details.credit_card_company }}">
                                                            </td>
                                                            <td style="padding:0 0 0 10px;">
                                                              <p class="mb-center" style="box-sizing: border-box; line-height: 1.5; margin: 0; text-align: left; color: {{ shop.email_accent_color }}; font-size: 16px;">
                                                                <span>
                                                                  ending with
                                                                  {{ transaction.payment_details.credit_card_last_four_digits }}
                                                                  &mdash;
                                                                  <strong>{{ transaction.amount | money }}</strong>
                                                                </span>
                                                              </p>
                                                            </td>
                                                          </tr>
                                                        </table>
                                                      {% elsif transaction.gateway_display_name == "Gift card" %}
                                                        <table role="presentation" style="border-collapse:collapse;border:0;border-spacing:0;margin: 0; text-align: left; color: {{ shop.email_accent_color }}; font-size: 16px;">
                                                          <tr>
                                                            <td style="padding:0;width:24px;">
                                                              <img src="{{ transaction.gateway_display_name | downcase | replace: ' ', '-' | payment_type_img_url }}" style="height: 24px;display: inline-block;margin-right: 10px;margin-top: 5px;margin-bottom: -6px;" height="24">
                                                            </td>
                                                            <td style="padding:0 0 0 10px;">
                                                              <p class="mb-center" style="box-sizing: border-box; line-height: 1.5; margin: 0; text-align: left; color: {{ shop.email_accent_color }}; font-size: 16px;">
                                                                <span>
                                                                  ending with
                                                                  {{ transaction.payment_details.gift_card.last_four_characters | upcase }}
                                                                  &mdash;
                                                                  <strong>{{ transaction.amount | money }}</strong>
                                                                </span>
                                                                <br>
                                                                &emsp;&emsp;&emsp;&nbsp;Gift card balance:
                                                                {{ transaction.payment_details.gift_card.balance | money }}
                                                              </p>
                                                            </td>
                                                          </tr>
                                                        </table>
                                                      {% else %}
                                                        <p class="mb-center" style="box-sizing: border-box; line-height: 1.5; margin: 0; text-align: left; color: {{ shop.email_accent_color }}; font-size: 16px;">
                                                          {{ transaction.gateway_display_name }} &mdash;
                                                          <strong>{{ transaction.amount | money }}</strong>
                                                        </p>
                                                      {% endif %}
                                                    {% endif %}
                                                  {% endif %}
                                                {% endfor %}
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                    </tr>
                                  </tbody>
                                </table>
                              </td>
                            </tr>
                          </tbody>
                        </table>
                      </td>
                    </tr>

                    <!-- Product item Info -->
                    {% for line in subtotal_line_items %}
                      {% if line.product.title %}
                        {% assign line_title = line.product.title %}
                      {% else %}
                        {% assign line_title = line.title %}
                      {% endif %}

                      {% if line.quantity < line.quantity %}
                        {% capture line_display %}
                          {{ line.quantity }} of {{ line.quantity }}
                        {% endcapture %}
                      {% else %}
                        {% assign line_display = line.quantity %}
                      {% endif %}

                      <tr class="mobile-only" style="box-sizing: border-box; mso-hide: all;">
                        <td style="background: #ffffff; box-sizing: border-box; display: none; font-size: 15px; line-height: 15px;" height="41"></td>
                      </tr>

                      <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                        <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                          <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                            <tbody style="box-sizing: border-box;">
                              <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                  <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                    <tbody style="box-sizing: border-box;">
                                      <tr class="row-wrap" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                        <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 20px; padding-left: 15px; padding-right: 15px; padding-top: 45px;" width="25%" align="left">
                                          <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                            <tbody style="box-sizing: border-box;">
                                              <tr class="show-all" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                                <td class="mb-center" align="left" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                                                  {% if line.image %}
                                                    <a alt="" target="_blank" class="image-link-wrapper" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; display: block; height: auto; max-width: 100%; width: 100%;">
                                                      <img src="{{ line | img_url: 'compact_cropped' }}" align="top" width="104" border="0" style="box-sizing: border-box; height: auto; width: 104px; border-radius: 8px; border: 1px solid #e5e5e5;">
                                                    </a>
                                                  {% endif %}
                                                </td>
                                              </tr>
                                            </tbody>
                                          </table>
                                        </td>
                                        <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 20px; padding-left: 15px; padding-right: 15px; padding-top: 45px;" width="50%" align="left">
                                          <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                            <tbody style="box-sizing: border-box;">
                                              <tr class="show-all" style="box-sizing: border-box; color: #000;">
                                                <td class="pr-0" style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 10px 10px 10px 0px; padding-bottom: 10px; padding-left: 0px; padding-right: 10px; padding-top: 10px;">
                                                  {% if line.product.title %}
                                                    {% assign line_title = line.product.title %}
                                                  {% else %}
                                                    {% assign line_title = line.title %}
                                                  {% endif %}

                                                  {% if line.quantity < line.quantity %}
                                                    {% capture line_display %}
                                                      {{ line.quantity }} of {{ line.quantity }}
                                                    {% endcapture %}
                                                  {% else %}
                                                    {% assign line_display = line.quantity %}
                                                  {% endif %}

                                                  <div style="box-sizing: border-box; line-height: normal;">
                                                    <p style="box-sizing: border-box; line-height: 1.5; margin: 0; text-align: justify;" class="mb-center">
                                                      <span style="box-sizing: border-box; color: rgb(0,0,0); font-size: 16px;">
                                                        {{ line_title }}&nbsp;&times;&nbsp;{{ line_display }}
                                                      </span>
                                                    </p>

                                                    {% if line.variant.title != 'Default Title' %}
                                                      <p style="box-sizing: border-box; line-height: 1.5; margin: 0; text-align: justify;" class="mb-center">
                                                        <span style="box-sizing: border-box; color: #8A8A8A; font-size: 14px;">
                                                          {{ line.variant.title }}
                                                        </span>
                                                      </p>
                                                    {% endif %}

                                                    {% if line.selling_plan_allocation %}
                                                      <p style="box-sizing: border-box; line-height: 1.5; margin: 0; text-align: justify;" class="mb-center">
                                                        <span style="box-sizing: border-box; color: #8A8A8A; font-size: 14px;">
                                                          {{ line.selling_plan_allocation.selling_plan.name }}
                                                        </span>
                                                      </p>
                                                    {% endif %}

                                                    {% if line.refunded_quantity > 0 %}
                                                      <p style="box-sizing: border-box; line-height: 1.5; margin: 0; text-align: justify;" class="mb-center">
                                                        <span style="box-sizing: border-box; color: #8A8A8A; font-size: 14px;">
                                                          Refunded
                                                        </span>
                                                      </p>
                                                    {% endif %}

                                                    {% if line.discount_allocations %}
                                                      {% for discount_allocation in line.discount_allocations %}
                                                        {% if discount_allocation.discount_application.target_selection != 'all' %}
                                                          <p style="color: #8A8A8A; font-size: 14px; box-sizing: border-box; line-height: 1.5; margin: 0; text-align: justify;" class="mb-center">
                                                            <img style="vertical-align: middle; margin-right: 6px;" src="{{ 'notifications/discounttag.png' | shopify_asset_url }}" width="18" height="18">
                                                            <span>
                                                              {{ discount_allocation.discount_application.title | upcase }}
                                                              (-{{ discount_allocation.amount | money }})
                                                            </span>
                                                          </p>
                                                        {% endif %}
                                                      {% endfor %}
                                                    {% endif %}
                                                  </div>
                                                </td>
                                              </tr>
                                            </tbody>
                                          </table>
                                        </td>
                                        <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 20px; padding-left: 15px; padding-right: 15px; padding-top: 45px;" width="25%" align="left">
                                          <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                            <tbody style="box-sizing: border-box;">
                                              <tr class="show-all" style="box-sizing: border-box; color: #000;">
                                                <td class="pl-0" style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 10px 0px 10px 0px; padding-bottom: 10px; padding-left: 0px; padding-right: 0px; padding-top: 10px;">
                                                  <div style="box-sizing: border-box; line-height: normal;">
                                                    {% if line.original_line_price != line.final_line_price %}
                                                      <p class="mb-center" style="box-sizing: border-box; line-height: 1.5; margin: 0; text-align: right;">
                                                        <span style="box-sizing: border-box; color: #8A8A8A; font-size: 14px;">
                                                          <s style="box-sizing: border-box;">
                                                            {{- line.original_line_price | money -}}
                                                          </s>
                                                        </span>
                                                      </p>
                                                    {% endif %}

                                                    <p class="mb-center" style="box-sizing: border-box; line-height: 1.5; margin: 0; text-align: right;">
                                                      {% if line.final_line_price > 0 %}
                                                        <strong style="box-sizing: border-box;">
                                                          {{- line.final_line_price | money -}}
                                                        </strong>
                                                      {% else %}
                                                        <strong style="box-sizing: border-box;">Free</strong>
                                                      {% endif %}
                                                    </p>

                                                    <p style="box-sizing: border-box; margin: 0;">&nbsp;</p>
                                                  </div>
                                                </td>
                                              </tr>
                                            </tbody>
                                          </table>
                                        </td>
                                      </tr>
                                    </tbody>
                                  </table>
                                </td>
                              </tr>
                            </tbody>
                          </table>
                        </td>
                      </tr>
                      <tr style="box-sizing: border-box; max-width: 100%;">
                        <td align="center" class="divider-padding" style="box-sizing: border-box; mso-padding-alt: 15px 0px; padding: 15px 0px;">
                          <table cellspacing="0" cellpadding="0" align="center" width="66%" style="border: 0; border-collapse: collapse; border-spacing: 0; box-sizing: border-box;" border="0">
                            <tbody style="box-sizing: border-box;">
                              <tr style="box-sizing: border-box;">
                                <td align="center" class="divider-line-2" style="background: #F1F1F1; box-sizing: border-box; font-size: 2px; line-height: 2px;" height="2"></td>
                              </tr>
                            </tbody>
                          </table>
                        </td>
                      </tr>
                    {% endfor %}

                    <!-- Products total prices -->
                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                      <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                        <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                          <tbody style="box-sizing: border-box;">
                            <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                              <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                  <tbody style="box-sizing: border-box;">
                                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                      <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 15px;" width="50%" align="left">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="box-sizing: border-box; color: #000;">
                                              <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 10px 40px 0px 15px; padding-bottom: 0px; padding-left: 15px; padding-right: 40px; padding-top: 10px;">
                                                <div style="box-sizing: border-box; line-height: normal;">
                                                  <p style="box-sizing: border-box; margin: 0;">
                                                    <span style="box-sizing: border-box; color: #363636; font-size: 16px;">Subtotal</span>
                                                  </p>
                                                </div>
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                      <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 15px;" width="50%" align="left">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="box-sizing: border-box; color: #000;">
                                              <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 10px 15px 0px 40px; padding-bottom: 0px; padding-left: 40px; padding-right: 15px; padding-top: 10px;">
                                                <div style="box-sizing: border-box; line-height: normal;">
                                                  <p style="box-sizing: border-box; margin: 0; text-align: right;">
                                                    <strong style="box-sizing: border-box;">
                                                      {{- subtotal_price | money -}}
                                                    </strong>
                                                  </p>
                                                </div>
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                    </tr>
                                  </tbody>
                                </table>
                              </td>
                            </tr>
                          </tbody>
                        </table>
                      </td>
                    </tr>

                    {% if delivery_method == 'pick-up' %}
                      <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                        <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                          <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                            <tbody style="box-sizing: border-box;">
                              <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                  <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                    <tbody style="box-sizing: border-box;">
                                      <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                        <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 15px;" width="50%" align="left">
                                          <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                            <tbody style="box-sizing: border-box;">
                                              <tr style="box-sizing: border-box; color: #000;">
                                                <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 40px 0px 15px; padding-bottom: 0px; padding-left: 15px; padding-right: 40px; padding-top: 0px;">
                                                  <div style="box-sizing: border-box; line-height: normal;">
                                                    <p style="box-sizing: border-box; margin: 0;">
                                                      <span style="box-sizing: border-box; color: #363636;">Pickup</span>
                                                    </p>
                                                  </div>
                                                </td>
                                              </tr>
                                            </tbody>
                                          </table>
                                        </td>
                                        <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 15px;" width="50%" align="left">
                                          <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                            <tbody style="box-sizing: border-box;">
                                              <tr style="box-sizing: border-box; color: #000;">
                                                <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 15px 0px 40px; padding-bottom: 0px; padding-left: 40px; padding-right: 15px; padding-top: 0px;">
                                                  <div style="box-sizing: border-box; line-height: normal;">
                                                    <p style="box-sizing: border-box; margin: 0; text-align: right;">
                                                      <strong style="box-sizing: border-box;">
                                                        {{- shipping_price | money -}}
                                                      </strong>
                                                    </p>
                                                  </div>
                                                </td>
                                              </tr>
                                            </tbody>
                                          </table>
                                        </td>
                                      </tr>
                                    </tbody>
                                  </table>
                                </td>
                              </tr>
                            </tbody>
                          </table>
                        </td>
                      </tr>
                    {% else %}
                      <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                        <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                          <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                            <tbody style="box-sizing: border-box;">
                              <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                  <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                    <tbody style="box-sizing: border-box;">
                                      <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                        <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 15px;" width="50%" align="left">
                                          <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                            <tbody style="box-sizing: border-box;">
                                              <tr style="box-sizing: border-box; color: #000;">
                                                <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 40px 0px 15px; padding-bottom: 0px; padding-left: 15px; padding-right: 40px; padding-top: 0px;">
                                                  <div style="box-sizing: border-box; line-height: normal;">
                                                    <p style="box-sizing: border-box; margin: 0;">
                                                      <span style="box-sizing: border-box; color: #363636;">Shipping</span>
                                                    </p>
                                                  </div>
                                                </td>
                                              </tr>
                                            </tbody>
                                          </table>
                                        </td>
                                        <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 15px;" width="50%" align="left">
                                          <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                            <tbody style="box-sizing: border-box;">
                                              <tr style="box-sizing: border-box; color: #000;">
                                                <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 15px 0px 40px; padding-bottom: 0px; padding-left: 40px; padding-right: 15px; padding-top: 0px;">
                                                  <div style="box-sizing: border-box; line-height: normal;">
                                                    <p style="box-sizing: border-box; margin: 0; text-align: right;">
                                                      <strong style="box-sizing: border-box;">
                                                        {{- shipping_price | money -}}
                                                      </strong>
                                                    </p>
                                                  </div>
                                                </td>
                                              </tr>
                                            </tbody>
                                          </table>
                                        </td>
                                      </tr>
                                    </tbody>
                                  </table>
                                </td>
                              </tr>
                            </tbody>
                          </table>
                        </td>
                      </tr>
                    {% endif %}

                    {% if total_duties %}
                      <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                        <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                          <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                            <tbody style="box-sizing: border-box;">
                              <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                  <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                    <tbody style="box-sizing: border-box;">
                                      <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                        <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 15px;" width="50%" align="left">
                                          <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                            <tbody style="box-sizing: border-box;">
                                              <tr style="box-sizing: border-box; color: #000;">
                                                <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 40px 0px 15px; padding-bottom: 0px; padding-left: 15px; padding-right: 40px; padding-top: 0px;">
                                                  <div style="box-sizing: border-box; line-height: normal;">
                                                    <p style="box-sizing: border-box; margin: 0;">
                                                      <span style="box-sizing: border-box; color: #363636;">Duties</span>
                                                    </p>
                                                  </div>
                                                </td>
                                              </tr>
                                            </tbody>
                                          </table>
                                        </td>
                                        <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 15px;" width="50%" align="left">
                                          <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                            <tbody style="box-sizing: border-box;">
                                              <tr style="box-sizing: border-box; color: #000;">
                                                <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 15px 0px 40px; padding-bottom: 0px; padding-left: 40px; padding-right: 15px; padding-top: 0px;">
                                                  <div style="box-sizing: border-box; line-height: normal;">
                                                    <p style="box-sizing: border-box; margin: 0; text-align: right;">
                                                      <strong style="box-sizing: border-box;">
                                                        {{- total_duties | money -}}
                                                      </strong>
                                                    </p>
                                                  </div>
                                                </td>
                                              </tr>
                                            </tbody>
                                          </table>
                                        </td>
                                      </tr>
                                    </tbody>
                                  </table>
                                </td>
                              </tr>
                            </tbody>
                          </table>
                        </td>
                      </tr>
                    {% endif %}

                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                      <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                        <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                          <tbody style="box-sizing: border-box;">
                            <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                              <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                  <tbody style="box-sizing: border-box;">
                                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                      <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 15px;" width="50%" align="left">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="box-sizing: border-box; color: #000;">
                                              <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 40px 0px 15px; padding-bottom: 0px; padding-left: 15px; padding-right: 40px; padding-top: 0px;">
                                                <div style="box-sizing: border-box; line-height: normal;">
                                                  <p style="box-sizing: border-box; margin: 0;">
                                                    <span style="box-sizing: border-box; color: #363636;">Taxes</span>
                                                  </p>
                                                </div>
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                      <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 15px;" width="50%" align="left">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="box-sizing: border-box; color: #000;">
                                              <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 15px 0px 40px; padding-bottom: 0px; padding-left: 40px; padding-right: 15px; padding-top: 0px;">
                                                <div style="box-sizing: border-box; line-height: normal;">
                                                  <p style="box-sizing: border-box; margin: 0; text-align: right;">
                                                    <strong style="box-sizing: border-box;">
                                                      {{- tax_price | money -}}
                                                    </strong>
                                                  </p>
                                                </div>
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                    </tr>
                                  </tbody>
                                </table>
                              </td>
                            </tr>
                          </tbody>
                        </table>
                      </td>
                    </tr>

                    {% if total_tip and total_tip > 0 %}
                      <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                        <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                          <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                            <tbody style="box-sizing: border-box;">
                              <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                  <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                    <tbody style="box-sizing: border-box;">
                                      <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                        <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 15px;" width="50%" align="left">
                                          <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                            <tbody style="box-sizing: border-box;">
                                              <tr style="box-sizing: border-box; color: #000;">
                                                <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 40px 0px 15px; padding-bottom: 0px; padding-left: 15px; padding-right: 40px; padding-top: 0px;">
                                                  <div style="box-sizing: border-box; line-height: normal;">
                                                    <p style="box-sizing: border-box; margin: 0;">
                                                      <span style="box-sizing: border-box; color: #363636;">Tip</span>
                                                    </p>
                                                  </div>
                                                </td>
                                              </tr>
                                            </tbody>
                                          </table>
                                        </td>
                                        <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 15px;" width="50%" align="left">
                                          <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                            <tbody style="box-sizing: border-box;">
                                              <tr style="box-sizing: border-box; color: #000;">
                                                <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 15px 0px 40px; padding-bottom: 0px; padding-left: 40px; padding-right: 15px; padding-top: 0px;">
                                                  <div style="box-sizing: border-box; line-height: normal;">
                                                    <p style="box-sizing: border-box; margin: 0; text-align: right;">
                                                      <strong style="box-sizing: border-box;">
                                                        {{- total_tip | money -}}
                                                      </strong>
                                                    </p>
                                                  </div>
                                                </td>
                                              </tr>
                                            </tbody>
                                          </table>
                                        </td>
                                      </tr>
                                    </tbody>
                                  </table>
                                </td>
                              </tr>
                            </tbody>
                          </table>
                        </td>
                      </tr>
                    {% endif %}

                    <tr style="box-sizing: border-box; max-width: 100%;">
                      <td align="center" class="divider-padding" style="box-sizing: border-box; mso-padding-alt: 15px 0px; padding: 15px 0px;">
                        <table cellspacing="0" cellpadding="0" align="center" width="66%" style="border: 0; border-collapse: collapse; border-spacing: 0; box-sizing: border-box;" border="0">
                          <tbody style="box-sizing: border-box;">
                            <tr style="box-sizing: border-box;">
                              <td align="center" class="divider-line-2" style="background: #F1F1F1; box-sizing: border-box; font-size: 2px; line-height: 2px;" height="2"></td>
                            </tr>
                          </tbody>
                        </table>
                      </td>
                    </tr>

                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                      <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                        <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                          <tbody style="box-sizing: border-box;">
                            <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                              <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                  <tbody style="box-sizing: border-box;">
                                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                      <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 15px; padding-left: 0px; padding-right: 0px; padding-top: 0px;" width="50%">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr class="show-all" style="box-sizing: border-box; color: #000;">
                                              <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 40px 0px 15px; padding-bottom: 0px; padding-left: 15px; padding-right: 40px; padding-top: 0px;">
                                                <div style="box-sizing: border-box; line-height: normal;">
                                                  <p style="box-sizing: border-box; margin: 0;">
                                                    <span style="box-sizing: border-box; font-size: 20px;">Total</span>
                                                  </p>
                                                </div>
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                      <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 15px; padding-left: 0px; padding-right: 0px; padding-top: 0px;" width="50%">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr class="show-all" style="box-sizing: border-box; color: #000;">
                                              <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 15px 0px 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 15px; padding-top: 0px;">
                                                <div style="box-sizing: border-box; line-height: normal;">
                                                  <p style="box-sizing: border-box; line-height: 1.15; margin: 0; text-align: right;">
                                                    <span style="box-sizing: border-box; font-size: 20px;"><strong style="box-sizing: border-box;">
                                                        {{- total_price | money_with_currency -}}
                                                      </strong></span>
                                                  </p>
                                                  <p style="color: #8A8A8A; font-size: 14px; box-sizing: border-box; line-height: 1.5; margin: 0;" align="right">
                                                    You saved
                                                    <span>
                                                      {{ total_discounts | money }}
                                                    </span>
                                                  </p>
                                                </div>
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                    </tr>
                                  </tbody>
                                </table>
                              </td>
                            </tr>
                          </tbody>
                        </table>
                      </td>
                    </tr>

                    {% assign transaction_size = 0 %}
                    {% assign transaction_amount = 0 %}
                    {% for transaction in transactions %}
                      {% unless transaction.kind == "capture" or transaction.kind == "void" %}
                        {% assign transaction_size = transaction_size | plus: 1 %}
                        {% assign transaction_amount = transaction_amount | plus: transaction.amount %}
                      {% endunless %}
                    {% endfor %}

                    {% if transaction_size > 1 or transaction_amount < total_price %}
                      <!-- Horizontal line -->
                      <tr style="box-sizing: border-box; max-width: 100%;">
                        <td align="center" class="divider-padding" style="box-sizing: border-box; mso-padding-alt: 15px 0px; padding: 15px 0px;">
                          <table cellspacing="0" cellpadding="0" align="center" width="100%" style="border: 0; border-collapse: collapse; border-spacing: 0; box-sizing: border-box;" border="0">
                            <tbody style="box-sizing: border-box;">
                              <tr style="box-sizing: border-box;">
                                <td align="center" class="divider-line-2" style="background: #F1F1F1; box-sizing: border-box; font-size: 2px; line-height: 2px;" height="2"></td>
                              </tr>
                            </tbody>
                          </table>
                        </td>
                      </tr>

                      {% for transaction in transactions %}
                        {% if transaction.status == "success" and transaction.kind == "authorization" or transaction.kind == "sale" %}
                          {% if transaction.payment_details.credit_card_company %}
                            {% capture transaction_name -%}
                              {{- transaction.payment_details.credit_card_company }} (ending in
                              {{ transaction.payment_details.credit_card_last_four_digits }})
                            {%- endcapture %}
                          {% else %}
                            {% capture transaction_name %}{{ transaction.gateway_display_name }}{% endcapture %}
                          {% endif %}

                          <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                            <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                              <table role="presentation" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed; margin: 0 auto;" width="100%" cellspacing="0" cellpadding="0" border="0">
                                <tbody style="box-sizing: border-box;">
                                  <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                    <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;" width="100%">
                                      <table role="presentation" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed; margin: 0 auto;" width="100%" cellspacing="0" cellpadding="0" border="0">
                                        <tbody style="box-sizing: border-box;">
                                          <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                            <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 15px 0px 0px;" width="50%" valign="middle" align="left">
                                              <table role="presentation" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed; margin: 0 auto;" width="100%" cellspacing="0" cellpadding="0" border="0">
                                                <tbody style="box-sizing: border-box;">
                                                  <tr style="box-sizing: border-box; color: #000;">
                                                    <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 40px 0px 15px; padding: 0px 40px 0px 15px;">
                                                      <div style="box-sizing: border-box; line-height: normal;">
                                                        <p style="box-sizing: border-box; margin: 0;">
                                                          <span style="box-sizing: border-box; color: #363636;">
                                                            {{- transaction_name -}}
                                                          </span>
                                                        </p>
                                                      </div>
                                                    </td>
                                                  </tr>
                                                </tbody>
                                              </table>
                                            </td>
                                            <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 15px 0px 0px;" width="50%" valign="middle" align="left">
                                              <table role="presentation" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed; margin: 0 auto;" width="100%" cellspacing="0" cellpadding="0" border="0">
                                                <tbody style="box-sizing: border-box;">
                                                  <tr style="box-sizing: border-box; color: #000;">
                                                    <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 15px 0px 40px; padding: 0px 15px 0px 40px;">
                                                      <div style="box-sizing: border-box; line-height: normal;">
                                                        <p style="box-sizing: border-box; margin: 0;" align="right">
                                                          <strong style="box-sizing: border-box;">
                                                            {{- transaction.amount | money -}}
                                                          </strong>
                                                        </p>
                                                      </div>
                                                    </td>
                                                  </tr>
                                                </tbody>
                                              </table>
                                            </td>
                                          </tr>
                                        </tbody>
                                      </table>
                                    </td>
                                  </tr>
                                </tbody>
                              </table>
                            </td>
                          </tr>
                        {% endif %}

                        {% if transaction.kind == 'refund' %}
                          {% if transaction.payment_details.credit_card_company %}
                            {% assign refund_method_title = transaction.payment_details.credit_card_company %}
                          {% else %}
                            {% assign refund_method_title = transaction.gateway %}
                          {% endif %}

                          <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                            <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                              <table role="presentation" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed; margin: 0 auto;" width="100%" cellspacing="0" cellpadding="0" border="0">
                                <tbody style="box-sizing: border-box;">
                                  <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                    <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;" width="100%">
                                      <table role="presentation" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed; margin: 0 auto;" width="100%" cellspacing="0" cellpadding="0" border="0">
                                        <tbody style="box-sizing: border-box;">
                                          <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                            <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 15px 0px 0px;" width="50%" valign="middle" align="left">
                                              <table role="presentation" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed; margin: 0 auto;" width="100%" cellspacing="0" cellpadding="0" border="0">
                                                <tbody style="box-sizing: border-box;">
                                                  <tr style="box-sizing: border-box; color: #000;">
                                                    <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 40px 0px 15px; padding: 0px 40px 0px 15px;">
                                                      <div style="box-sizing: border-box; line-height: normal;">
                                                        <p style="box-sizing: border-box; margin: 0; color: #363636;">
                                                          <span>Refund</span><br>
                                                          <small>{{ refund_method_title | capitalize }}</small>
                                                        </p>
                                                      </div>
                                                    </td>
                                                  </tr>
                                                </tbody>
                                              </table>
                                            </td>
                                            <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 15px 0px 0px;" width="50%" valign="middle" align="left">
                                              <table role="presentation" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed; margin: 0 auto;" width="100%" cellspacing="0" cellpadding="0" border="0">
                                                <tbody style="box-sizing: border-box;">
                                                  <tr style="box-sizing: border-box; color: #000;">
                                                    <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 0px 15px 0px 40px; padding: 0px 15px 0px 40px;">
                                                      <div style="box-sizing: border-box; line-height: normal;">
                                                        <p style="box-sizing: border-box; margin: 0;" align="right">
                                                          <strong style="box-sizing: border-box;">- {{ transaction.amount | money -}}
                                                          </strong>
                                                        </p>
                                                      </div>
                                                    </td>
                                                  </tr>
                                                </tbody>
                                              </table>
                                            </td>
                                          </tr>
                                        </tbody>
                                      </table>
                                    </td>
                                  </tr>
                                </tbody>
                              </table>
                            </td>
                          </tr>
                        {% endif %}
                      {% endfor %}
                    {% endif %}
                    <!-- Discount offer -->
                    <tr style="box-sizing: border-box;">
                      <td style="box-sizing: border-box; font-size: 15px; line-height: 15px;" height="30"></td>
                    </tr>
                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; background: #f7f7f7; box-sizing: border-box;">
                      <td style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                        <table role="presentation" cellspacing="0" border="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                          <tbody style="box-sizing: border-box;">
                            <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                              <td width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 0;">
                                <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                                  <tbody style="box-sizing: border-box;">
                                    <tr class="row-wrap" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                      <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;" width="50%">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                                              <td align="center" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                                                <a alt="" target="_blank" class="image-link-wrapper" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; display: block; height: auto; max-width: 100%; width: 100%;"><img src="{{ discount_image }}" align="top" width="100%" height="auto" loading="lazy" border="0" style="box-sizing: border-box; height: auto; width: 100%;"></a>
                                              </td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                      <td valign="middle" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 0px;" width="50%">
                                        <table role="presentation" border="0" cellspacing="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellpadding="0">
                                          <tbody style="box-sizing: border-box;">
                                            <tr style="box-sizing: border-box; color: #000;">
                                              <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 30px 0px 0px 0px; padding-bottom: 0px; padding-left: 0px; padding-right: 0px; padding-top: 30px;">
                                                <div style="box-sizing: border-box; line-height: normal;">
                                                  <p style="box-sizing: border-box; line-height: 1.5; margin: 0; text-align: center;">
                                                    <span style="box-sizing: border-box; color: #636363; font-size: 18px;"><strong style="box-sizing: border-box;">FOR YOUR NEXT PURCHASE</strong></span>
                                                  </p>
                                                  <p style="box-sizing: border-box; line-height: 1.5; margin: 5px 0; text-align: center;">
                                                    <span style="box-sizing: border-box; color: #414141; font-size: 48px;"><strong style="box-sizing: border-box;">
                                                        {{- amount_off -}}
                                                      </strong></span>
                                                  </p>
                                                  <p style="box-sizing: border-box; line-height: 1.5; margin: 0; text-align: center;">
                                                    <span style="box-sizing: border-box; color: #636363; font-size: 16px;">USE THE CODE: &nbsp;</span><span style="box-sizing: border-box; color: {{ shop.email_accent_color }}; font-size: 16px;">
                                                      {{- discount_code -}}
                                                    </span>
                                                  </p>
                                                </div>
                                              </td>
                                            </tr>
                                            <tr style="box-sizing: border-box;">
                                              <td style="box-sizing: border-box; font-size: 15px; line-height: 15px;" height="30"></td>
                                            </tr>
                                            <tr style="box-sizing: border-box;">
                                              <td align="center" style="box-sizing: border-box;">
                                                <table cellpadding="0" align="center" width="100%" style="border: 0; border-collapse: collapse; border-spacing: 0; box-sizing: border-box;" border="0" cellspacing="0">
                                                  <tbody style="box-sizing: border-box;">
                                                    <tr style="box-sizing: border-box;">
                                                      <td align="center" style="box-sizing: border-box;">
                                                        <table cellspacing="0" cellpadding="0" align="center" class="button-container" style="border: 0; border-collapse: collapse; border-spacing: 0; box-sizing: border-box;" border="0">
                                                          <tbody style="box-sizing: border-box;">
                                                            <tr style="box-sizing: border-box;">
                                                              <td align="center" style="background: #333333; border-radius: 20px; border-style: solid; border-width: 0px; box-sizing: border-box; display: block; mso-padding-alt: 10px 45px 10px 45px;">
                                                                <a target="_blank" href="{{ shop.url }}" style="box-sizing: border-box; color: #ffffff; display: block; font-size: 13px; font-weight: 400; letter-spacing: 1px; padding-bottom: 10px; padding-left: 45px; padding-right: 45px; padding-top: 10px; text-decoration: none; white-space: nowrap;">
                                                                  SHOP SOME MORE</a>
                                                              </td>
                                                            </tr>
                                                          </tbody>
                                                        </table>
                                                      </td>
                                                    </tr>
                                                  </tbody>
                                                </table>
                                              </td>
                                            </tr>
                                            <tr style="box-sizing: border-box;">
                                              <td style="box-sizing: border-box; font-size: 15px; line-height: 15px;" height="30"></td>
                                            </tr>
                                          </tbody>
                                        </table>
                                      </td>
                                    </tr>
                                  </tbody>
                                </table>
                              </td>
                            </tr>
                          </tbody>
                        </table>
                      </td>
                    </tr>
                    <tr style="box-sizing: border-box;">
                      <td style="box-sizing: border-box; font-size: 15px; line-height: 15px;" height="30"></td>
                    </tr>
                    <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                      <td valign="middle" align="center" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt; padding: 15px;">
                        <table role="presentation" border="0" cellpadding="0" width="100%" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; border-collapse: collapse; border-spacing: 0; box-sizing: border-box; margin: 0 auto; mso-table-lspace: 0pt; mso-table-rspace: 0pt; table-layout: fixed;" cellspacing="0">
                          <tbody style="box-sizing: border-box;">
                            <tr style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box;">
                              <td valign="middle" align="center" class="logo" style="-ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%; box-sizing: border-box; mso-table-lspace: 0pt; mso-table-rspace: 0pt;">
                                <a href="{{ shop.url }}" target="_blank" style="box-sizing: border-box; max-width: 100%;">
                                  {%- if shop.email_logo_url %}
                                    <img width="{{ shop.email_logo_width }}" src="{{ shop.email_logo_url }}" alt="{{ shop.name }}" style="-ms-interpolation-mode: bicubic; box-sizing: border-box; display: block; height: auto; margin: auto; outline: none; text-decoration: none;">
                                  {%- else %}
                                    <h2 style="font-weight: normal; font-size: 30px; color: #333; margin: 0;">
                                      {{ shop.name }}
                                    </h2>
                                  {%- endif %}
                                </a>
                              </td>
                            </tr>
                          </tbody>
                        </table>
                      </td>
                    </tr>
                    <tr style="box-sizing: border-box;">
                      <td align="center" class="divider-padding" style="box-sizing: border-box; mso-padding-alt: 15px 0px; padding: 15px 0px;">
                        <table cellspacing="0" cellpadding="0" align="center" width="66%" style="border: 0; border-collapse: collapse; border-spacing: 0; box-sizing: border-box;" border="0">
                          <tbody style="box-sizing: border-box;">
                            <tr style="box-sizing: border-box;">
                              <td align="center" class="divider-line-2" style="background: #F1F1F1; box-sizing: border-box; font-size: 2px; line-height: 2px;" height="2"></td>
                            </tr>
                          </tbody>
                        </table>
                      </td>
                    </tr>
                    <tr style="box-sizing: border-box; color: #000;">
                      <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 10px 40px 10px 40px; padding-bottom: 10px; padding-left: 40px; padding-right: 40px; padding-top: 10px;">
                        <div style="box-sizing: border-box; line-height: normal;">
                          <p style="box-sizing: border-box; margin: 0; text-align: center;">
                            <span style="box-sizing: border-box; color: #999999; font-size: 12px;">If you have any questions, reply to this email or <br>
                              contact us at
                            </span>
                            <span style="box-sizing: border-box; color: {{ shop.email_accent_color }}; font-size: 12px;">
                              <a style="text-decoration: underline; color: {{ shop.email_accent_color }};font-size: 12px;" href="mailto:{{ shop.email }}" target="_blank">
                                {{ shop.email }}
                              </a>
                            </span>
                          </p>
                        </div>
                      </td>
                    </tr>
                    <tr style="box-sizing: border-box;">
                      <td align="center" class="divider-padding" style="box-sizing: border-box; mso-padding-alt: 15px 0px; padding: 15px 0px;"></td>
                    </tr>

                    <tr style="box-sizing: border-box; background-color: #333333">
                      <td style="box-sizing: border-box; font-family: Roboto, Tahoma, Verdana, Segoe, sans-serif; mso-padding-alt: 10px 40px 10px 40px; padding-bottom: 10px; padding-left: 40px; padding-right: 40px; padding-top: 10px;">
                        <div style="box-sizing: border-box; line-height: normal;">
                          <p style="box-sizing: border-box; margin: 0; text-align: center;">
                            <span style="box-sizing: border-box; color: #bbbbbb; font-size: 12px;">Designed and developed by
                            </span>
                            <span style="box-sizing: border-box; color: {{ shop.email_accent_color }}; font-size: 12px;">
                              <a style="text-decoration: underline; color: #ffffff;font-size: 12px;" href="https://www.doudmine.com/" target="_blank">
                                Doudmine
                              </a>
                            </span>
                          </p>
                        </div>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </td>
            </tr>
          </tbody>
        </table>
      </center>
      <link href="https://fonts.googleapis.com/css?family=Roboto" rel="stylesheet" style="box-sizing: border-box;">
    </body>
  </body>
</html>
```
3. Upload your logo and 2 image assets in **Settings** > **Files**. One image for banner and other for a Discount offer
4. Watch the video below to see how you can customize the new email Order Confirmation template

{{< youtube KNY8lwaEvo8 >}}

That's it! I hope this tutorial has been helpful and if you need something don't hesitate to [contact me](https://www.doudmine.com/contact/) 
