---
author: Driss Oudmine
title: Hype your products with this beautiful coming soon page for Shopify - No app
description: In this step by step tutorial you will learn how to add a coming soon page to your Shopify store using code.
date: 2022-05-07
thumbnail: /coming-soon
---
You start a business or product and plan to launch it on Shopify, you want the interest of potential customers to amplify your reach before opening, then creating a great Shopify coming soon page is one of the best ways to start collecting qualified shoppers and give your business a much-needed boost in the early days of trading. With a sizable list of prospective customers to market to, you’ll have excellent referral potential, more conversions, and more revenue from day one. 

In this article, I'm going to guide you to implement a good looking coming soon page to your Shopify store without the need of an app! So let's get started


1. From your Shopify admin, go to **Online Store** > **Themes**.
2. Find the Dawn theme, and then click **Actions** > **Duplicate**.
3. Find the theme that called _Copy of Dawn_ then click **Actions** > **Edit Code**.
4. On the left bar, search for a folder called _templates_ then delete a file called "password.json".
5. After you delete the file "password.json" create a new one called "password.liquid". The difference between the two is the new file has ".liquid" at the end. 
6. Copy and the paste the following code inside the "password.liquid" file:
```html {linenos=table}
{% layout none %}
<!doctype html>
<html class="no-js" lang="{{ request.locale.iso_code }}">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <meta name="theme-color" content="">
    <link rel="canonical" href="{{ canonical_url }}">
    <link rel="preconnect" href="https://cdn.shopify.com" crossorigin>

    {%- if settings.favicon != blank -%}
      <link rel="icon" type="image/png" href="{{ settings.favicon | image_url: width: 32, height: 32 }}">
    {%- endif -%}

    {%- unless settings.type_header_font.system? and settings.type_body_font.system? -%}
      <link rel="preconnect" href="https://fonts.shopifycdn.com" crossorigin>
    {%- endunless -%}

    <title>
      {{ page_title }}
      {%- if current_tags %} &ndash; tagged "{{ current_tags | join: ', ' }}"{% endif -%}
      {%- if current_page != 1 %} &ndash; Page {{ current_page }}{% endif -%}
      {%- unless page_title contains shop.name %} Coming soon &ndash; {{ shop.name }}{% endunless -%}
    </title>

    {% if page_description %}
      <meta name="description" content="{{ page_description | escape }}">
    {% endif %}

    {% render 'meta-tags' %}

    <!-- CSS
    ================================================== -->
    <link rel="stylesheet" href="{{ 'vendor__LP.css' | asset_url }}">
    <link rel="stylesheet" href="{{ 'style__LP.css' | asset_url }}">

    {% style %}
    :root {
      --color-base-accent-2: {{ settings.colors_accent_2.red }}, {{ settings.colors_accent_2.green }}, {{ settings.colors_accent_2.blue }};
    }
    {% endstyle %}

    <!-- scripts
    ================================================== -->
    <script
      src="https://cdnjs.cloudflare.com/ajax/libs/modernizr/2.8.3/modernizr.min.js"
      defer
    ></script>
    <script
      src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/js/all.min.js"
      defer
    ></script>

    <script
      src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.min.js"
      defer
    ></script>
    
    <script src="{{ 'plugins__LP.min.js' | asset_url }}" defer="defer"></script>
    <script src="{{ 'script__LP.js' | asset_url }}" defer="defer"></script>

    {{ content_for_header }}
  </head>

  <body id="top">
    <!-- preloader
    ==================================================--> 
    <div id="preloader">
      <div id="loader" class="dots-fade">
        <div></div>
        <div></div>
        <div></div>
      </div>
    </div>
    
    {% form 'customer', class: 'form__header' %}
      {% if form.posted_successfully? %}
        <p for="mc-email" class="subscribe-message">Thank you for subscribing</p>
        {%- endif -%}
    {% endform %}
    
    {%- section 'header__LP' -%}

    <main>
      {%- section 'banner__LP' -%}
      {%- section 'info__LP' -%}
    </main>
  </body>
</html>
```
7. Again on the left bar, search for a folder called _Sections_ then create a new file called "header__LP".
8. Copy and paste the following code inside the "header__LP" file:
```html {linenos=table}
<!-- page header
================================================== -->
<header class="s-header">
  <div class="header-logo">
    <a class="site-logo" href="index.html">
      {%- if section.settings.logo != blank -%}
        {%- assign image_size = section.settings.logo_width | append: 'x' -%}
        <img srcset="{{ section.settings.logo | img_url: image_size }} 1x, {{ section.settings.logo | img_url: image_size, scale: 2 }} 2x"
          src="{{ section.settings.logo | img_url: image_size }}"
          loading="lazy"
          width="{{ section.settings.logo_width }}"
          alt="{{ section.settings.logo.alt | default: shop.name | escape }}"
        >
      {%- else -%}
        <span class="site-logo__name">{{ shop.name }}</span>
      {%- endif -%}
    </a>
  </div>

  <div class="header-email">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="24"
      height="24"
      viewBox="0 0 24 24"
    >
      <path
        d="M0 12l11 3.1 7-8.1-8.156 5.672-4.312-1.202 15.362-7.68-3.974 14.57-3.75-3.339-2.17 2.925v-.769l-2-.56v7.383l4.473-6.031 4.527 4.031 6-22z"
      />
    </svg>
    <a href="mailto:{{ section.settings.email }}">{{ section.settings.email }}</a>
  </div>
</header>
<!-- end s-header -->

{% schema %}
{
  "name": "Header",
  "settings": [
    {
      "type": "image_picker",
      "id": "logo",
      "label": "t:sections.header.settings.logo.label"
    },
    {
      "type": "range",
      "id": "logo_width",
      "min": 50,
      "max": 250,
      "step": 10,
      "default": 140,
      "unit": "t:sections.header.settings.logo_width.unit",
      "label": "t:sections.header.settings.logo_width.label"
    },
    {
      "type": "text",
      "id": "email",
      "label": "Create your email",
      "default": "contact@domainame.com"
    }
  ]
}
{% endschema %}
```
9. Next, create a new file called "banner__LP" in the _Sections_ folder.
10. Copy and paste the following code inside the "banner__LP" file:
```html {linenos=table}
{% style %}
  .s-intro--static {
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
    background-image: url("{{ section.settings.banner-img | img_url: '2000x' }}");
  }
{% endstyle %}
<!-- intro
================================================== -->
<section id="intro" class="s-intro s-intro--static">
  <div class="grid-overlay">
    <div></div>
  </div>

  <div class="row intro-content">
    <div class="column">
      <div class="intro-content__text">
        <h3>{{ section.settings.subtext }}</h3>

        <h1>{{ section.settings.text }}</h1>
      </div>
      <!-- end intro-content__text -->

      <div class="intro-content__bottom">
        <div class="intro-content__counter-wrap">
          <h4>Launching in</h4>

          <div class="counter" data-time="{{section.settings.countdown}}">
            <div class="counter__time days">
              365
              <span>D</span>
            </div>
            <div class="counter__time hours">
              09
              <span>H</span>
            </div>
            <div class="counter__time minutes">
              54
              <span>M</span>
            </div>
            <div class="counter__time seconds">
              57
              <span>S</span>
            </div>
          </div>
          <!-- end counter -->
        </div>
        <!-- end intro-content__counter-wrap -->

        <div class="intro-content__notify">
          <button
            type="button"
            class="btn--stroke btn--small modal-trigger"
          >
            Notify Me
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
            >
              <path d="M24 12l-9-9v7h-15v4h15v7z" />
            </svg>
          </button>
        </div>
        <!-- end intro-content__notify -->
      </div>
      <!-- end intro-content__bottom -->
    </div>
    <!-- end column -->
  </div>
  <!--  end intro-content -->

  <div class="modal">
    <div class="modal__inner">
      <span class="modal__close"></span>

      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
      >
        <path
          d="M0 3v18h24v-18h-24zm6.623 7.929l-4.623 5.712v-9.458l4.623 3.746zm-4.141-5.929h19.035l-9.517 7.713-9.518-7.713zm5.694 7.188l3.824 3.099 3.83-3.104 5.612 6.817h-18.779l5.513-6.812zm9.208-1.264l4.616-3.741v9.348l-4.616-5.607z"
        />
      </svg>

      <h3>Sign Up</h3>
      <p>
        Be the first to know about the latest updates and get exclusive
        offer on our grand opening.
      </p>

      {% form 'customer', class: 'group mc-form' %}
        <input type="hidden" name="contact[tags]" value="newsletter">
        <div>
          <input
            id="NewsletterForm--{{ section.id }}"
            type="email"
            name="contact[email]"
            class="email h-full-width h-text-center h-add-half-bottom"
            aria-required="true"
            autocorrect="off"
            autocapitalize="off"
            autocomplete="email"
            {% if form.errors %}
              autofocus
              aria-invalid="true"
              aria-describedby="Newsletter-error--{{ section.id }}"
            {% elsif form.posted_successfully? %}
              aria-describedby="Newsletter-success--{{ section.id }}"
            {% endif %}
            placeholder="{{ 'newsletter.label' | t }}"
            required
          >
          <input
            type="submit"
            name="commit"
            value="Subscribe"
            class="btn--small h-full-width"
          />
        </div>
        {%- if form.errors -%}
          <small class="newsletter-form__message form__message" id="Newsletter-error--{{ section.id }}">{{ form.errors.translated_fields['email'] | capitalize }} {{ form.errors.messages['email'] }}</small>
        {% elsif form.posted_successfully? %}
          <label for="mc-email" class="subscribe-message">Thank you for subscribing</label>
        {%- endif -%}
      {% endform %}
    </div>
    <!-- end modal inner -->
  </div>
  <!-- end modal -->

  <ul class="intro-social" role="list">
    {%- if settings.social_twitter_link != blank -%}
      <li>
        <a href="{{ settings.social_twitter_link }}">
          <i class="fab fa-twitter" aria-hidden="true"></i>
        </a>
      </li>
    {%- endif -%}
    {%- if settings.social_facebook_link != blank -%}
      <li>
        <a href="{{ settings.social_facebook_link }}">
          <i class="fab fa-facebook" aria-hidden="true"></i>
        </a>
      </li>
    {%- endif -%}
    {%- if settings.social_pinterest_link != blank -%}
      <li>
        <a href="{{ settings.social_pinterest_link }}">
          <i class="fab fa-pinterest" aria-hidden="true"></i>
        </a>
      </li>
    {%- endif -%}
    {%- if settings.social_instagram_link != blank -%}
      <li>
        <a href="{{ settings.social_instagram_link }}">
          <i class="fab fa-instagram" aria-hidden="true"></i>
        </a>
      </li>
    {%- endif -%}
    {%- if settings.social_tiktok_link != blank -%}
      <li>
        <a href="{{ settings.social_tiktok_link }}">
          <i class="fab fa-tiktok" aria-hidden="true"></i>
        </a>
      </li>
    {%- endif -%}
    {%- if settings.social_tumblr_link != blank -%}
      <li>
        <a href="{{ settings.social_tumblr_link }}">
          <i class="fab fa-tumblr" aria-hidden="true"></i>
        </a>
      </li>
    {%- endif -%}
    {%- if settings.social_snapchat_link != blank -%}
      <li>
        <a href="{{ settings.social_snapchat_link }}">
          <i class="fab fa-snapchat" aria-hidden="true"></i>
        </a>
      </li>
    {%- endif -%}
    {%- if settings.social_youtube_link != blank -%}
      <li>
        <a href="{{ settings.social_youtube_link }}">
          <i class="fab fa-youtube" aria-hidden="true"></i>
        </a>
      </li>
    {%- endif -%}
    {%- if settings.social_vimeo_link != blank -%}
      <li>
        <a href="{{ settings.social_vimeo_link }}">
          <i class="fab fa-vimeo" aria-hidden="true"></i>
        </a>
      </li>
    {%- endif -%}
  </ul>
  <!-- end intro social -->

  <div class="intro-scroll">
    <a href="#info" class="scroll-link smoothscroll"> Scroll For More </a>
  </div>
  <!-- end intro scroll -->
</section>
<!-- end s-intro -->

{% schema %}
{
  "name": "Banner",
  "settings": [
    {
      "type": "image_picker",
      "id": "banner-img",
      "label": "Select an image banner"
    },
    {
      "type": "text",
      "id": "subtext",
      "label": "Create your subtext",
      "default": "Subtext here"
    },
    {
      "type": "text",
      "id": "text",
      "label": "Create your text banner",
      "default": "Tempora debitis perspiciatis eum. Repudiandae et aperiam quos exercitationem enim voluptatem quam sequi temporibus."
    },
    {
      "type": "text",
      "id": "countdown",
      "label": "Countdown timer",
      "default": "2022/05/29",
      "info": "Please respect this date format YYYY/MM/DD"
    }
  ]
}
{% endschema %}
```
11. Again, create a new file called "info__LP" and paste the following code inside it:
```html {linenos=table}
<!-- info
================================================== -->
<section id="info" class="s-info">
  <div class="vert-line"></div>

  <div class="row info-content">
    <div class="column">
      <nav class="tab-nav">
        <ul class="tab-nav__list">
          {%- for block in section.blocks -%}
          {% case block.type %}
          {% when 'about' %}
          <li class="active" data-id="tab-about">
            <a href="#0" {{ block.shopify_attributes }}>
              <span>{{block.settings.about}}</span>
            </a>
          </li>
          {% when 'products' %}
          <li data-id="tab-products">
            <a href="#0" {{ block.shopify_attributes }}>
              <span>{{block.settings.products}}</span>
            </a>
          </li>
          {% when 'contact' %}
          <li data-id="tab-contact">
            <a href="#0" {{ block.shopify_attributes }}>
              <span>{{block.settings.contact}}</span>
            </a>
          </li>
          {% endcase %}
          {%- endfor -%}
        </ul>
      </nav>
      <!-- end tab-nav -->

      <div class="tab-content">
        {%- for block in section.blocks -%}
        {% case block.type %}
        {% when 'about' %}
        <!-- 01. tab about -->
        <div id="tab-about" class="tab-content__item">
          <div class="row tab-content__item-header">
            <div class="column">
              <h2>{{block.settings.about_title}}</h2>
            </div>
          </div>

          <div class="row">
            <div class="column">
              {% if block.settings.paragraph_one != blank %}
              <p class="lead">
                {{block.settings.paragraph_one}}
              </p>
              {% endif %}

              {% if block.settings.paragraph_two != blank %}
              <p>
                {{block.settings.paragraph_two}}
              </p>
              {% endif %}

              {% if block.settings.title_paragraph_three != blank %}
              <div class="row">
                <div class="column large-6 tab-full">
                  <h4>{{block.settings.title_paragraph_three}}</h4>
                  <p>
                    {{block.settings.paragraph_three}}
                  </p>
                </div>

                {% if block.settings.title_paragraph_four != blank %}
                <div class="column large-6 tab-full">
                  <h4>{{block.settings.title_paragraph_four}}</h4>
                  <p>
                    {{block.settings.paragraph_four}}
                  </p>
                </div>
                {% endif %}
              </div>
              {% endif %}
            </div>
          </div>
        </div>
        {% when 'products' %}
        <!-- 02. tab products -->
        <div id="tab-products" class="tab-content__item">
          <div class="row tab-content__item-header">
            <div class="column">
              <h2>{{block.settings.products_title}}</h2>
            </div>
          </div>

          <div class="row">
            <div class="column">
              <p class="lead">
                {{block.settings.products_paragraph}}
              </p>
            </div>
          </div>

          <div
            class="row services-list block-large-1-2 block-medium-1-2 block-tab-full"
          >
            {% if block.settings.title_product_1 != blank %}
            <div class="column services-list__item">
              <div class="services-list__item-content">
                <h4 class="item-title">{{block.settings.title_product_1}}</h4>
                <p>
                  {{block.settings.des_product_1}}
                </p>
              </div>
            </div>
            {% endif %}

            {% if block.settings.title_product_2 != blank %}
            <div class="column services-list__item">
              <div class="services-list__item-content">
                <h4 class="item-title">{{block.settings.title_product_2}}</h4>
                <p>
                  {{block.settings.des_product_2}}
                </p>
              </div>
            </div>
            {% endif %}

            {% if block.settings.title_product_3 != blank %}
            <div class="column services-list__item">
              <div class="services-list__item-content">
                <h4 class="item-title">{{block.settings.title_product_3}}</h4>
                <p>
                  {{block.settings.des_product_3}}
                </p>
              </div>
            </div>
            {% endif %}

            {% if block.settings.title_product_4 != blank %}
            <div class="column services-list__item">
              <div class="services-list__item-content">
                <h4 class="item-title">{{block.settings.title_product_4}}</h4>
                <p>
                  {{block.settings.des_product_4}}
                </p>
              </div>
            </div>
            {% endif %}
          </div>
          <!-- end services-list -->
        </div>
        {% when 'contact' %}
        <!-- 03. tab contact -->
        <div id="tab-contact" class="tab-content__item">
          <div class="row tab-content__item-header">
            <div class="column">
              <h2>{{block.settings.main_title}}</h2>
            </div>
          </div>

          <div class="row">
            <div class="column">
              <p class="lead">
                {{block.settings.main_paragraph}}
              </p>

              <div class="row">
                <div class="column large-six tab-full">
                  <h4>{{block.settings.address_title}}</h4>

                  
                  <p>{{block.settings.address}}</p>
                  
                </div>

                {%- if settings.social_twitter_link != blank -%}
                <div class="column large-six tab-full">
                  <h4>Follow Us</h4>

                  <ul class="link-list">
                    {%- if settings.social_twitter_link != blank -%}
                    <li>
                      <a href="{{ settings.social_twitter_link }}">
                        Twitter
                      </a>
                    </li>
                    {%- endif -%}
                    {%- if settings.social_facebook_link != blank -%}
                      <li>
                        <a href="{{ settings.social_facebook_link }}">
                          Facebook
                        </a>
                      </li>
                    {%- endif -%}
                    {%- if settings.social_pinterest_link != blank -%}
                      <li>
                        <a href="{{ settings.social_pinterest_link }}">
                          Pinterest
                        </a>
                      </li>
                    {%- endif -%}
                    {%- if settings.social_instagram_link != blank -%}
                      <li>
                        <a href="{{ settings.social_instagram_link }}">
                          Instagram
                        </a>
                      </li>
                    {%- endif -%}
                    {%- if settings.social_tiktok_link != blank -%}
                      <li>
                        <a href="{{ settings.social_tiktok_link }}">
                          Tiktok
                        </a>
                      </li>
                    {%- endif -%}
                    {%- if settings.social_tumblr_link != blank -%}
                      <li>
                        <a href="{{ settings.social_tumblr_link }}">
                          Tumblr
                        </a>
                      </li>
                    {%- endif -%}
                    {%- if settings.social_snapchat_link != blank -%}
                      <li>
                        <a href="{{ settings.social_snapchat_link }}">
                          Snapchat
                        </a>
                      </li>
                    {%- endif -%}
                    {%- if settings.social_youtube_link != blank -%}
                      <li>
                        <a href="{{ settings.social_youtube_link }}">
                          Youtube
                        </a>
                      </li>
                    {%- endif -%}
                    {%- if settings.social_vimeo_link != blank -%}
                      <li>
                        <a href="{{ settings.social_vimeo_link }}">
                          Vimeo
                        </a>
                      </li>
                    {%- endif -%}
                  </ul>
                </div>
                {%- endif -%}
              </div>

              <p class="tab-content__item-bottom">
                <a href="mailto:{{block.settings.email}}" class="contact-email"
                  >{{block.settings.email}}</a
                >
                <span class="contact-number">
                  <a href="tel:{{block.settings.number_1}}">{{block.settings.number_1}}</a>
                  {%- if block.settings.number_2 != blank -%}
                  <a href="tel:{{block.settings.number_2}}">{{block.settings.number_2}}</a>
                  {%- endif -%}
                </span>
              </p>
            </div>
          </div>
        </div>
        {% endcase %}
        {%- endfor -%}
      </div>
      <!-- end tab content -->

      <footer>
        <div class="ss-copyright">
          <span>© Copyright Imminent 2019</span>
          <span
            >Design by
            <a href="https://www.styleshout.com/">StyleShout</a></span
          >
        </div>

        <div class="ss-go-top">
          <a class="smoothscroll" title="Back to Top" href="#top">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
            >
              <path d="M12 0l8 9h-6v15h-4v-15h-6z"></path>
            </svg>
          </a>
        </div>
      </footer>
    </div>
    <!-- end column -->
  </div>
  <!-- end row -->
</section>
<!-- end s-info -->

{% schema %}
{
  "name": "Tabs",
  "class": "index-section",
  "max_blocks": 3,
  "settings": [],
  "blocks": [
    {
      "type": "about",
      "name": "About",
      "settings": [
        {
          "type": "text",
          "id": "about",
          "label": "Nav name",
          "default": "About"
        },
        {
          "type": "header",
          "content": "Tab content"
        },
        {
          "type": "text",
          "id": "about_title",
          "label": "About title",
          "default": "Hello. We are Imminent."
        },
        {
          "type": "textarea",
          "id": "paragraph_one",
          "label": "First paragraph",
          "default": "Quidem molestiae natus ipsa ut nihil molestiae numquam tenetur. Ipsum quia sit vitae ipsam et temporibus est. Consequatur recusandae aut aut. Aut esse sed sint. Sit ipsa velit possimus est. Atque doloribus dicta sit beatae necessitatibus."
        },
        {
          "type": "textarea",
          "id": "paragraph_two",
          "label": "Second paragraph",
          "default": "Tempora debitis perspiciatis eum. Repudiandae et aperiam quos exercitationem enim voluptatem quam sequi temporibus. Ratione quis nihil voluptatem placeat nemo. Quibusdam delectus magni quas et architecto et repellat a nam. Quasi et voluptates libero sed vel quos in nisi. Error et quis. Impedit autem porro facilis. Aut voluptate asperiores nostrum eveniet magnam et consequatur ab accusamus. Consequatur quod ut omnis eum dicta mollitia dignissimos."
        },
        {
          "type": "text",
          "id": "title_paragraph_three",
          "label": "Title of third paragraph",
          "default": "Title here."
        },
        {
          "type": "textarea",
          "id": "paragraph_three",
          "label": "Third paragraph",
          "default": "Tempora debitis perspiciatis eum. Repudiandae et aperiam quos exercitationem enim voluptatem quam sequi temporibus. Ratione quis nihil voluptatem placeat nemo. Quibusdam delectus magni quas et architecto et repellat a nam. Quasi et voluptates libero sed vel quos in nisi. Error et quis. Impedit autem porro facilis."
        },
        {
          "type": "text",
          "id": "title_paragraph_four",
          "label": "Title of fourth paragraph",
          "default": "Title here."
        },
        {
          "type": "textarea",
          "id": "paragraph_four",
          "label": "Fourth paragraph",
          "default": "Tempora debitis perspiciatis eum. Repudiandae et aperiam quos exercitationem enim voluptatem quam sequi temporibus. Ratione quis nihil voluptatem placeat nemo. Quibusdam delectus magni quas et architecto et repellat a nam. Quasi et voluptates libero sed vel quos in nisi. Error et quis. Impedit autem porro facilis."
        }
      ]
    },
    {
      "type": "products",
      "name": "Products",
      "settings": [
        {
          "type": "text",
          "id": "products",
          "label": "Nav name",
          "default": "Products"
        },
        {
          "type": "header",
          "content": "Tab content"
        },
        {
          "type": "text",
          "id": "products_title",
          "label": "Main title",
          "default": "Main title here."
        },
        {
          "type": "textarea",
          "id": "products_paragraph",
          "label": "Main paragraph",
          "default": "Tempora debitis perspiciatis eum. Repudiandae et aperiam quos exercitationem enim voluptatem quam sequi temporibus. Ratione quis nihil voluptatem placeat nemo."
        },
        {
          "type": "header",
          "content": "First product"
        },
        {
          "type": "text",
          "id": "title_product_1",
          "label": "Title of first product",
          "default": "Title here."
        },
        {
          "type": "textarea",
          "id": "des_product_1",
          "label": "Description of first product",
          "default": "Tempora debitis perspiciatis eum. Repudiandae et aperiam quos exercitationem enim voluptatem quam sequi temporibus. Ratione quis nihil voluptatem placeat nemo."
        },
        {
          "type": "header",
          "content": "Second product"
        },
        {
          "type": "text",
          "id": "title_product_2",
          "label": "Title of second product",
          "default": "Title here."
        },
        {
          "type": "textarea",
          "id": "des_product_2",
          "label": "Description of second product",
          "default": "Tempora debitis perspiciatis eum. Repudiandae et aperiam quos exercitationem enim voluptatem quam sequi temporibus. Ratione quis nihil voluptatem placeat nemo."
        },
        {
          "type": "header",
          "content": "Third product"
        },
        {
          "type": "text",
          "id": "title_product_3",
          "label": "Title of third product",
          "default": "Title here."
        },
        {
          "type": "textarea",
          "id": "des_product_3",
          "label": "Description of third product",
          "default": "Tempora debitis perspiciatis eum. Repudiandae et aperiam quos exercitationem enim voluptatem quam sequi temporibus. Ratione quis nihil voluptatem placeat nemo."
        },
        {
          "type": "header",
          "content": "Fourth product"
        },
        {
          "type": "text",
          "id": "title_product_4",
          "label": "Title of fourth product",
          "default": "Title here."
        },
        {
          "type": "textarea",
          "id": "des_product_4",
          "label": "Description of fourth product",
          "default": "Tempora debitis perspiciatis eum. Repudiandae et aperiam quos exercitationem enim voluptatem quam sequi temporibus. Ratione quis nihil voluptatem placeat nemo."
        }
      ]
    },
    {
      "type": "contact",
      "name": "Contact",
      "settings": [
        {
          "type": "text",
          "id": "contact",
          "label": "Nav name",
          "default": "Contact"
        },
        {
          "type": "header",
          "content": "Tab content"
        },
        {
          "type": "text",
          "id": "main_title",
          "label": "Main title",
          "default": "Main title here."
        },
        {
          "type": "textarea",
          "id": "main_paragraph",
          "label": "Main paragraph",
          "default": "Tempora debitis perspiciatis eum. Repudiandae et aperiam quos exercitationem enim voluptatem quam sequi temporibus. Ratione quis nihil voluptatem placeat nemo."
        },
        {
          "type": "text",
          "id": "address_title",
          "label": "Title for address",
          "default": "Title here."
        },
        {
          "type": "html",
          "id": "address",
          "label": "Bussiness address",
          "default": "1600 Amphitheatre Parkway <br>Mountain View, CA<br>94043 US",
          "info": "The <br> tag inserts a single line break."
        },
        {
          "type": "text",
          "id": "email",
          "label": "Email address",
          "default": "hello@domainame.com"
        },
        {
          "type": "text",
          "id": "number_1",
          "label": "Contact number 1",
          "default": "+197 543 2345"
        },
        {
          "type": "text",
          "id": "number_2",
          "label": "Contact number 2",
          "default": "+197 543 2345"
        }
      ]
    }
  ],
  "default": {
    "settings": {},
    "blocks": [
      {
        "type": "about"
      },
      {
        "type": "products"
      },
      {
        "type": "contact"
      }
    ]
  }
}
{% endschema %}
```
12. Next on the left bar, search for a folder called _Assets_ then create a file called "vendor__LP.css".
13. After you created the file "vendor__LP.css" paste the following code inside it:
```css {linenos=table}
/* =================================================================== 
 *  Imminent Base Stylesheet
 *  Ver. 1.0.0
 *  09-19-2019
 *  ------------------------------------------------------------------
 *
 *  TOC:
 *	# imports 
 *	# normalize
 *	# basic/base setup styles
 *	# grid v2.1.1
 *	# block grids
 *	# MISC
 *
 * =================================================================== */

/* ===================================================================
 * # imports 
 *
 * ------------------------------------------------------------------- */
@import url("https://fonts.googleapis.com/css?family=DM+Serif+Display:400,400i|Gothic+A1:300,400,500,600,700,800&display=swap");

/* ==========================================================================
  * # normalize
  * normalize.css v8.0.1 | MIT License |
  * github.com/necolas/normalize.css
  *
  * -------------------------------------------------------------------------- */

/* ------------------------------------------------------------------- 
  * ## document
  * ------------------------------------------------------------------- */

/* 1. Correct the line height in all browsers.
  * 2. Prevent adjustments of font size after orientation changes in iOS.*/
html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* ------------------------------------------------------------------- 
  * ## sections
  * ------------------------------------------------------------------- */

/* Remove the margin in all browsers. */
body {
  margin: 0;
}

/* Render the `main` element consistently in IE. */
main {
  display: block;
}

/* Correct the font size and margin on `h1` elements within `section` and
  * `article` contexts in Chrome, Firefox, and Safari. */
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* ------------------------------------------------------------------- 
  * ## grouping
  * ------------------------------------------------------------------- */

/* 1. Add the correct box sizing in Firefox.
  * 2. Show the overflow in Edge and IE. */
hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/* 1. Correct the inheritance and scaling of font size in all browsers.
  * 2. Correct the odd `em` font sizing in all browsers. */
pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* ------------------------------------------------------------------- 
  * ## text-level semantics
  * ------------------------------------------------------------------- */

/* Remove the gray background on active links in IE 10. */
a {
  background-color: transparent;
}

/* 1. Remove the bottom border in Chrome 57-
  * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari. */
abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/* Add the correct font weight in Chrome, Edge, and Safari. */
b,
strong {
  font-weight: bolder;
}

/* 1. Correct the inheritance and scaling of font size in all browsers.
  * 2. Correct the odd `em` font sizing in all browsers. */
code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Add the correct font size in all browsers. */
small {
  font-size: 80%;
}

/* Prevent `sub` and `sup` elements from affecting the line height in
  * all browsers. */
sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* ------------------------------------------------------------------- 
  * ## embedded content
  * ------------------------------------------------------------------- */

/* Remove the border on images inside links in IE 10. */
img {
  border-style: none;
}

/* ------------------------------------------------------------------- 
  * ## forms
  * ------------------------------------------------------------------- */

/* 1. Change the font styles in all browsers.
  * 2. Remove the margin in Firefox and Safari. */
button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/* Show the overflow in IE.
  * 1. Show the overflow in Edge. */
button,
input {
  /* 1 */
  overflow: visible;
}

/* Remove the inheritance of text transform in Edge, Firefox, and IE.
  * 1. Remove the inheritance of text transform in Firefox. */
button,
select {
  /* 1 */
  text-transform: none;
}

/* Correct the inability to style clickable types in iOS and Safari. */
button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/* Remove the inner border and padding in Firefox. */
button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/* Restore the focus styles unset by the previous rule. */
button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/* Correct the padding in Firefox. */
fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/* 1. Correct the text wrapping in Edge and IE.
  * 2. Correct the color inheritance from `fieldset` elements in IE.
  * 3. Remove the padding so developers are not caught out when they zero out
  *    `fieldset` elements in all browsers. */
legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/* Add the correct vertical alignment in Chrome, Firefox, and Opera. */
progress {
  vertical-align: baseline;
}

/* Remove the default vertical scrollbar in IE 10+. */
textarea {
  overflow: auto;
}

/* 1. Add the correct box sizing in IE 10.
  * 2. Remove the padding in IE 10. */
[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/* Correct the cursor style of increment and decrement buttons in Chrome. */
[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/* 1. Correct the odd appearance in Chrome and Safari.
  * 2. Correct the outline style in Safari. */
[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/* Remove the inner padding in Chrome and Safari on macOS. */
[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/* 1. Correct the inability to style clickable types in iOS and Safari.
  * 2. Change font properties to `inherit` in Safari. */
::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* ------------------------------------------------------------------- 
  * ## interactive
  * ------------------------------------------------------------------- */

/* Add the correct display in Edge, IE 10+, and Firefox. */
details {
  display: block;
}

/* Add the correct display in all browsers. */
summary {
  display: list-item;
}

/* ------------------------------------------------------------------- 
  * ## misc
  * ------------------------------------------------------------------- */

/* Add the correct display in IE 10+. */
template {
  display: none;
}

/* Add the correct display in IE 10. */
[hidden] {
  display: none;
}

/* ===================================================================
  * # basic/base setup styles
  *
  * ------------------------------------------------------------------- */
html {
  font-size: 62.5%;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}

body {
  font-weight: normal;
  line-height: 1;
  word-wrap: break-word;
  -moz-font-smoothing: grayscale;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  -webkit-overflow-scrolling: touch;
  -webkit-text-size-adjust: none;
}

/* ------------------------------------------------------------------- 
  * ## Media
  * ------------------------------------------------------------------- */
svg,
img,
video embed,
iframe,
object {
  max-width: 100%;
  height: auto;
}

/* ------------------------------------------------------------------- 
  * ## Typography resets 
  * ------------------------------------------------------------------- */
div,
dl,
dt,
dd,
ul,
ol,
li,
h1,
h2,
h3,
h4,
h5,
h6,
pre,
form,
p,
blockquote,
th,
td {
  margin: 0;
  padding: 0;
}

p {
  font-size: inherit;
  text-rendering: optimizeLegibility;
}

em,
i {
  font-style: italic;
  line-height: inherit;
}

strong,
b {
  font-weight: bold;
  line-height: inherit;
}

small {
  font-size: 60%;
  line-height: inherit;
}

ol,
ul {
  list-style: none;
}

li {
  display: block;
}

/* ------------------------------------------------------------------- 
  * ## links
  * ------------------------------------------------------------------- */
a {
  text-decoration: none;
  line-height: inherit;
}

a img {
  border: none;
}

/* ------------------------------------------------------------------- 
  * ## inputs
  * ------------------------------------------------------------------- */
fieldset {
  margin: 0;
  padding: 0;
}

input[type="email"],
input[type="number"],
input[type="search"],
input[type="text"],
input[type="tel"],
input[type="url"],
input[type="password"],
textarea {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

/* ===================================================================
  * # grid v2.1.1
  *
  *   -----------------------------------------------------------------
  * - Grid breakpoints are based on MAXIMUM WIDTH media queries, 
  *   meaning they apply to that one breakpoint and ALL THOSE BELOW IT.
  * - Grid columns without a specified width will automatically layout 
  *   as equal width columns.
  * ------------------------------------------------------------------- */

/* rows
  * ------------------------------------- */
.row {
  width: 89%;
  max-width: 1400px;
  margin: 0 auto;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  -webkit-flex-flow: row wrap;
  -ms-flex-flow: row wrap;
  flex-flow: row wrap;
}

.row .row {
  width: auto;
  max-width: none;
  margin-left: -20px;
  margin-right: -20px;
}

/* columns
  * -------------------------------------- */
.column {
  -webkit-flex: 1 1 0%;
  -ms-flex: 1 1 0%;
  flex: 1 1 0%;
  padding: 0 20px;
}

.collapse > .column,
.column.collapse {
  padding: 0;
}

/* flex row containers utility classes
  * ----------------------------------------- */
.row.row-wrap {
  -webkit-flex-wrap: wrap;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
}

.row.row-nowrap {
  -webkit-flex-wrap: nowrap;
  -ms-flex-wrap: none;
  flex-wrap: nowrap;
}

.row.row-y-top {
  -webkit-align-items: flex-start;
  -ms-flex-align: start;
  align-items: flex-start;
}

.row.row-y-bottom {
  -webkit-align-items: flex-end;
  -ms-flex-align: end;
  align-items: flex-end;
}

.row.row-y-center {
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
}

.row.row-stretch {
  -webkit-align-items: stretch;
  -ms-flex-align: stretch;
  align-items: stretch;
}

.row.row-baseline {
  -webkit-align-items: baseline;
  -ms-flex-align: baseline;
  align-items: baseline;
}

.row.row-x-left {
  -ms-flex-pack: start;
  -webkit-justify-content: flex-start;
  justify-content: flex-start;
}

.row.row-x-right {
  -ms-flex-pack: end;
  -webkit-justify-content: flex-end;
  justify-content: flex-end;
}

.row.row-x-center {
  -ms-flex-pack: center;
  -webkit-justify-content: center;
  justify-content: center;
}

/* flex item utility alignment classes
  * ----------------------------------------- */
.align-center {
  margin: auto;
  -webkit-align-self: center;
  -ms-flex-item-align: center;
  align-self: center;
}

.align-left {
  margin-right: auto;
  -webkit-align-self: center;
  -ms-flex-item-align: center;
  align-self: center;
}

.align-right {
  margin-left: auto;
  -webkit-align-self: center;
  -ms-flex-item-align: center;
  align-self: center;
}

.align-x-center {
  margin-right: auto;
  margin-left: auto;
}

.align-x-left {
  margin-right: auto;
}

.align-x-right {
  margin-left: auto;
}

.align-y-center {
  -webkit-align-self: center;
  -ms-flex-item-align: center;
  align-self: center;
}

.align-y-top {
  -webkit-align-self: flex-start;
  -ms-flex-item-align: start;
  align-self: flex-start;
}

.align-y-bottom {
  -webkit-align-self: flex-end;
  -ms-flex-item-align: end;
  align-self: flex-end;
}

/* large screen column widths 
  * -------------------------------------- */
.large-1 {
  -webkit-flex: 0 0 8.33333%;
  -ms-flex: 0 0 8.33333%;
  flex: 0 0 8.33333%;
  max-width: 8.33333%;
}

.large-2 {
  -webkit-flex: 0 0 16.66667%;
  -ms-flex: 0 0 16.66667%;
  flex: 0 0 16.66667%;
  max-width: 16.66667%;
}

.large-3 {
  -webkit-flex: 0 0 25%;
  -ms-flex: 0 0 25%;
  flex: 0 0 25%;
  max-width: 25%;
}

.large-4 {
  -webkit-flex: 0 0 33.33333%;
  -ms-flex: 0 0 33.33333%;
  flex: 0 0 33.33333%;
  max-width: 33.33333%;
}

.large-5 {
  -webkit-flex: 0 0 41.66667%;
  -ms-flex: 0 0 41.66667%;
  flex: 0 0 41.66667%;
  max-width: 41.66667%;
}

.large-6,
.large-half {
  -webkit-flex: 0 0 50%;
  -ms-flex: 0 0 50%;
  flex: 0 0 50%;
  max-width: 50%;
}

.large-7 {
  -webkit-flex: 0 0 58.33333%;
  -ms-flex: 0 0 58.33333%;
  flex: 0 0 58.33333%;
  max-width: 58.33333%;
}

.large-8 {
  -webkit-flex: 0 0 66.66667%;
  -ms-flex: 0 0 66.66667%;
  flex: 0 0 66.66667%;
  max-width: 66.66667%;
}

.large-9 {
  -webkit-flex: 0 0 75%;
  -ms-flex: 0 0 75%;
  flex: 0 0 75%;
  max-width: 75%;
}

.large-10 {
  -webkit-flex: 0 0 83.33333%;
  -ms-flex: 0 0 83.33333%;
  flex: 0 0 83.33333%;
  max-width: 83.33333%;
}

.large-11 {
  -webkit-flex: 0 0 91.66667%;
  -ms-flex: 0 0 91.66667%;
  flex: 0 0 91.66667%;
  max-width: 91.66667%;
}

.large-12,
.large-full {
  -webkit-flex: 0 0 100%;
  -ms-flex: 0 0 100%;
  flex: 0 0 100%;
  max-width: 100%;
}

/* ------------------------------------------------------------------- 
  * ## medium screen devices
  * ------------------------------------------------------------------- */
@media screen and (max-width: 1200px) {
  .row .row {
    margin-left: -16px;
    margin-right: -16px;
  }

  .column {
    padding: 0 16px;
  }

  .medium-1 {
    -webkit-flex: 0 0 8.33333%;
    -ms-flex: 0 0 8.33333%;
    flex: 0 0 8.33333%;
    max-width: 8.33333%;
  }

  .medium-2 {
    -webkit-flex: 0 0 16.66667%;
    -ms-flex: 0 0 16.66667%;
    flex: 0 0 16.66667%;
    max-width: 16.66667%;
  }

  .medium-3 {
    -webkit-flex: 0 0 25%;
    -ms-flex: 0 0 25%;
    flex: 0 0 25%;
    max-width: 25%;
  }

  .medium-4 {
    -webkit-flex: 0 0 33.33333%;
    -ms-flex: 0 0 33.33333%;
    flex: 0 0 33.33333%;
    max-width: 33.33333%;
  }

  .medium-5 {
    -webkit-flex: 0 0 41.66667%;
    -ms-flex: 0 0 41.66667%;
    flex: 0 0 41.66667%;
    max-width: 41.66667%;
  }

  .medium-6,
  .medium-half {
    -webkit-flex: 0 0 50%;
    -ms-flex: 0 0 50%;
    flex: 0 0 50%;
    max-width: 50%;
  }

  .medium-7 {
    -webkit-flex: 0 0 58.33333%;
    -ms-flex: 0 0 58.33333%;
    flex: 0 0 58.33333%;
    max-width: 58.33333%;
  }

  .medium-8 {
    -webkit-flex: 0 0 66.66667%;
    -ms-flex: 0 0 66.66667%;
    flex: 0 0 66.66667%;
    max-width: 66.66667%;
  }

  .medium-9 {
    -webkit-flex: 0 0 75%;
    -ms-flex: 0 0 75%;
    flex: 0 0 75%;
    max-width: 75%;
  }

  .medium-10 {
    -webkit-flex: 0 0 83.33333%;
    -ms-flex: 0 0 83.33333%;
    flex: 0 0 83.33333%;
    max-width: 83.33333%;
  }

  .medium-11 {
    -webkit-flex: 0 0 91.66667%;
    -ms-flex: 0 0 91.66667%;
    flex: 0 0 91.66667%;
    max-width: 91.66667%;
  }

  .medium-12,
  .medium-full {
    -webkit-flex: 0 0 100%;
    -ms-flex: 0 0 100%;
    flex: 0 0 100%;
    max-width: 100%;
  }
}

/* ------------------------------------------------------------------- 
  * ## tablets
  * ------------------------------------------------------------------- */
@media screen and (max-width: 800px) {
  .tab-1 {
    -webkit-flex: 0 0 8.33333%;
    -ms-flex: 0 0 8.33333%;
    flex: 0 0 8.33333%;
    max-width: 8.33333%;
  }

  .tab-2 {
    -webkit-flex: 0 0 16.66667%;
    -ms-flex: 0 0 16.66667%;
    flex: 0 0 16.66667%;
    max-width: 16.66667%;
  }

  .tab-3 {
    -webkit-flex: 0 0 25%;
    -ms-flex: 0 0 25%;
    flex: 0 0 25%;
    max-width: 25%;
  }

  .tab-4 {
    -webkit-flex: 0 0 33.33333%;
    -ms-flex: 0 0 33.33333%;
    flex: 0 0 33.33333%;
    max-width: 33.33333%;
  }

  .tab-5 {
    -webkit-flex: 0 0 41.66667%;
    -ms-flex: 0 0 41.66667%;
    flex: 0 0 41.66667%;
    max-width: 41.66667%;
  }

  .tab-6,
  .tab-half {
    -webkit-flex: 0 0 50%;
    -ms-flex: 0 0 50%;
    flex: 0 0 50%;
    max-width: 50%;
  }

  .tab-7 {
    -webkit-flex: 0 0 58.33333%;
    -ms-flex: 0 0 58.33333%;
    flex: 0 0 58.33333%;
    max-width: 58.33333%;
  }

  .tab-8 {
    -webkit-flex: 0 0 66.66667%;
    -ms-flex: 0 0 66.66667%;
    flex: 0 0 66.66667%;
    max-width: 66.66667%;
  }

  .tab-9 {
    -webkit-flex: 0 0 75%;
    -ms-flex: 0 0 75%;
    flex: 0 0 75%;
    max-width: 75%;
  }

  .tab-10 {
    -webkit-flex: 0 0 83.33333%;
    -ms-flex: 0 0 83.33333%;
    flex: 0 0 83.33333%;
    max-width: 83.33333%;
  }

  .tab-11 {
    -webkit-flex: 0 0 91.66667%;
    -ms-flex: 0 0 91.66667%;
    flex: 0 0 91.66667%;
    max-width: 91.66667%;
  }

  .tab-12,
  .tab-full {
    -webkit-flex: 0 0 100%;
    -ms-flex: 0 0 100%;
    flex: 0 0 100%;
    max-width: 100%;
  }

  .hide-on-tablet {
    display: none;
  }
}

/* ------------------------------------------------------------------- 
  * ## mobile devices 
  * ------------------------------------------------------------------- */
@media screen and (max-width: 600px) {
  .row {
    width: 100%;
    padding-left: 25px;
    padding-right: 25px;
  }

  .row .row {
    margin-left: -10px;
    margin-right: -10px;
    padding-left: 0;
    padding-right: 0;
  }

  .column {
    padding: 0 10px;
  }

  .mob-1 {
    -webkit-flex: 0 0 8.33333%;
    -ms-flex: 0 0 8.33333%;
    flex: 0 0 8.33333%;
    max-width: 8.33333%;
  }

  .mob-2 {
    -webkit-flex: 0 0 16.66667%;
    -ms-flex: 0 0 16.66667%;
    flex: 0 0 16.66667%;
    max-width: 16.66667%;
  }

  .mob-3 {
    -webkit-flex: 0 0 25%;
    -ms-flex: 0 0 25%;
    flex: 0 0 25%;
    max-width: 25%;
  }

  .mob-4 {
    -webkit-flex: 0 0 33.33333%;
    -ms-flex: 0 0 33.33333%;
    flex: 0 0 33.33333%;
    max-width: 33.33333%;
  }

  .mob-5 {
    -webkit-flex: 0 0 41.66667%;
    -ms-flex: 0 0 41.66667%;
    flex: 0 0 41.66667%;
    max-width: 41.66667%;
  }

  .mob-6,
  .mob-half {
    -webkit-flex: 0 0 50%;
    -ms-flex: 0 0 50%;
    flex: 0 0 50%;
    max-width: 50%;
  }

  .mob-7 {
    -webkit-flex: 0 0 58.33333%;
    -ms-flex: 0 0 58.33333%;
    flex: 0 0 58.33333%;
    max-width: 58.33333%;
  }

  .mob-8 {
    -webkit-flex: 0 0 66.66667%;
    -ms-flex: 0 0 66.66667%;
    flex: 0 0 66.66667%;
    max-width: 66.66667%;
  }

  .mob-9 {
    -webkit-flex: 0 0 75%;
    -ms-flex: 0 0 75%;
    flex: 0 0 75%;
    max-width: 75%;
  }

  .mob-10 {
    -webkit-flex: 0 0 83.33333%;
    -ms-flex: 0 0 83.33333%;
    flex: 0 0 83.33333%;
    max-width: 83.33333%;
  }

  .mob-11 {
    -webkit-flex: 0 0 91.66667%;
    -ms-flex: 0 0 91.66667%;
    flex: 0 0 91.66667%;
    max-width: 91.66667%;
  }

  .mob-12,
  .mob-full {
    -webkit-flex: 0 0 100%;
    -ms-flex: 0 0 100%;
    flex: 0 0 100%;
    max-width: 100%;
  }

  .hide-on-mobile {
    display: none;
  }
}

/* ------------------------------------------------------------------- 
  * ## small mobile devices <= 400px
  * ------------------------------------------------------------------- */
@media screen and (max-width: 400px) {
  .row {
    padding-left: 22px;
    padding-right: 22px;
  }

  .row .row {
    margin-left: 0;
    margin-right: 0;
  }

  .column {
    -webkit-flex: 0 0 100%;
    -ms-flex: 0 0 100%;
    flex: 0 0 100%;
    max-width: 100%;
    width: 100%;
    margin-left: 0;
    margin-right: 0;
    padding: 0;
  }
}

/* ===================================================================
  * # block grids
  *
  * -------------------------------------------------------------------
  * Equally-sized columns define at parent/row level.
  * ------------------------------------------------------------------- */
.block-large-1-8 > .column {
  -webkit-flex: 0 0 12.5%;
  -ms-flex: 0 0 12.5%;
  flex: 0 0 12.5%;
  max-width: 12.5%;
}

.block-large-1-6 > .column {
  -webkit-flex: 0 0 16.66667%;
  -ms-flex: 0 0 16.66667%;
  flex: 0 0 16.66667%;
  max-width: 16.66667%;
}

.block-large-1-5 > .column {
  -webkit-flex: 0 0 20%;
  -ms-flex: 0 0 20%;
  flex: 0 0 20%;
  max-width: 20%;
}

.block-large-1-4 > .column {
  -webkit-flex: 0 0 25%;
  -ms-flex: 0 0 25%;
  flex: 0 0 25%;
  max-width: 25%;
}

.block-large-1-3 > .column {
  -webkit-flex: 0 0 33.33333%;
  -ms-flex: 0 0 33.33333%;
  flex: 0 0 33.33333%;
  max-width: 33.33333%;
}

.block-large-1-2 > .column {
  -webkit-flex: 0 0 50%;
  -ms-flex: 0 0 50%;
  flex: 0 0 50%;
  max-width: 50%;
}

.block-large-full > .column {
  -webkit-flex: 0 0 100%;
  -ms-flex: 0 0 100%;
  flex: 0 0 100%;
  max-width: 100%;
}

/* ------------------------------------------------------------------- 
  * ## block grids - medium screen devices
  * ------------------------------------------------------------------- */
@media screen and (max-width: 1200px) {
  .block-medium-1-8 > .column {
    -webkit-flex: 0 0 12.5%;
    -ms-flex: 0 0 12.5%;
    flex: 0 0 12.5%;
    max-width: 12.5%;
  }

  .block-medium-1-6 > .column {
    -webkit-flex: 0 0 16.66667%;
    -ms-flex: 0 0 16.66667%;
    flex: 0 0 16.66667%;
    max-width: 16.66667%;
  }

  .block-medium-1-5 > .column {
    -webkit-flex: 0 0 20%;
    -ms-flex: 0 0 20%;
    flex: 0 0 20%;
    max-width: 20%;
  }

  .block-medium-1-4 > .column {
    -webkit-flex: 0 0 25%;
    -ms-flex: 0 0 25%;
    flex: 0 0 25%;
    max-width: 25%;
  }

  .block-medium-1-3 > .column {
    -webkit-flex: 0 0 33.33333%;
    -ms-flex: 0 0 33.33333%;
    flex: 0 0 33.33333%;
    max-width: 33.33333%;
  }

  .block-medium-1-2 > .column {
    -webkit-flex: 0 0 50%;
    -ms-flex: 0 0 50%;
    flex: 0 0 50%;
    max-width: 50%;
  }

  .block-medium-full > .column {
    -webkit-flex: 0 0 100%;
    -ms-flex: 0 0 100%;
    flex: 0 0 100%;
    max-width: 100%;
  }
}

/* ------------------------------------------------------------------- 
  * ## block grids - tablets
  * ------------------------------------------------------------------- */
@media screen and (max-width: 800px) {
  .block-tab-1-8 > .column {
    -webkit-flex: 0 0 12.5%;
    -ms-flex: 0 0 12.5%;
    flex: 0 0 12.5%;
    max-width: 12.5%;
  }

  .block-tab-1-6 > .column {
    -webkit-flex: 0 0 16.66667%;
    -ms-flex: 0 0 16.66667%;
    flex: 0 0 16.66667%;
    max-width: 16.66667%;
  }

  .block-tab-1-5 > .column {
    -webkit-flex: 0 0 20%;
    -ms-flex: 0 0 20%;
    flex: 0 0 20%;
    max-width: 20%;
  }

  .block-tab-1-4 > .column {
    -webkit-flex: 0 0 25%;
    -ms-flex: 0 0 25%;
    flex: 0 0 25%;
    max-width: 25%;
  }

  .block-tab-1-3 > .column {
    -webkit-flex: 0 0 33.33333%;
    -ms-flex: 0 0 33.33333%;
    flex: 0 0 33.33333%;
    max-width: 33.33333%;
  }

  .block-tab-1-2 > .column {
    -webkit-flex: 0 0 50%;
    -ms-flex: 0 0 50%;
    flex: 0 0 50%;
    max-width: 50%;
  }

  .block-tab-full > .column {
    -webkit-flex: 0 0 100%;
    -ms-flex: 0 0 100%;
    flex: 0 0 100%;
    max-width: 100%;
  }
}

/* ------------------------------------------------------------------- 
  * ## block grids - mobile devices
  * ------------------------------------------------------------------- */
@media screen and (max-width: 600px) {
  .block-mob-1-8 > .column {
    -webkit-flex: 0 0 12.5%;
    -ms-flex: 0 0 12.5%;
    flex: 0 0 12.5%;
    max-width: 12.5%;
  }

  .block-mob-1-6 > .column {
    -webkit-flex: 0 0 16.66667%;
    -ms-flex: 0 0 16.66667%;
    flex: 0 0 16.66667%;
    max-width: 16.66667%;
  }

  .block-mob-1-5 > .column {
    -webkit-flex: 0 0 20%;
    -ms-flex: 0 0 20%;
    flex: 0 0 20%;
    max-width: 20%;
  }

  .block-mob-1-4 > .column {
    -webkit-flex: 0 0 25%;
    -ms-flex: 0 0 25%;
    flex: 0 0 25%;
    max-width: 25%;
  }

  .block-mob-1-3 > .column {
    -webkit-flex: 0 0 33.33333%;
    -ms-flex: 0 0 33.33333%;
    flex: 0 0 33.33333%;
    max-width: 33.33333%;
  }

  .block-mob-1-2 > .column {
    -webkit-flex: 0 0 50%;
    -ms-flex: 0 0 50%;
    flex: 0 0 50%;
    max-width: 50%;
  }

  .block-mob-full > .column {
    -webkit-flex: 0 0 100%;
    -ms-flex: 0 0 100%;
    flex: 0 0 100%;
    max-width: 100%;
  }
}

/* ------------------------------------------------------------------- 
  * ## block grids - small mobile devices <= 400px
  * ------------------------------------------------------------------- */
@media screen and (max-width: 400px) {
  .stack > .column {
    -webkit-flex: 0 0 100%;
    -ms-flex: 0 0 100%;
    flex: 0 0 100%;
    max-width: 100%;
    width: 100%;
    margin-left: 0;
    margin-right: 0;
    padding: 0;
  }
}

/* ===================================================================
  * # MISC
  *
  * ------------------------------------------------------------------- */
.h-group:after {
  content: "";
  display: table;
  clear: both;
}

/* misc helper classes
  * -------------------------------------- */
.is-hidden {
  display: none;
}

.is-invisible {
  visibility: hidden;
}

.h-antialiased {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.h-overflow-hidden {
  overflow: hidden;
}

.h-remove-bottom {
  margin-bottom: 0;
}

.h-add-half-bottom {
  margin-bottom: 1.6rem !important;
}

.h-add-bottom {
  margin-bottom: 3.2rem !important;
}

.h-no-border {
  border: none;
}

.h-full-width {
  width: 100%;
}

.h-text-center {
  text-align: center;
}

.h-text-left {
  text-align: left;
}

.h-text-right {
  text-align: right;
}

.h-pull-left {
  float: left;
}

.h-pull-right {
  float: right;
}

/*# sourceMappingURL=base.css.map */

/* =================================================================== 
 *  Imminent Vendor/Third Party CSS
 *  Template Ver. 1.0.0 
 *  09-19-2019
 *  ------------------------------------------------------------------
 *
 *  TOC:
 *  # slick slider
 *  # prettyprint GitHub Theme
 *
 * =================================================================== */

/* ===================================================================
 * # slick slider
 * http://kenwheeler.github.io/slick/
 * ------------------------------------------------------------------- */

/* Slider */
.slick-slider {
  position: relative;
  display: block;
  box-sizing: border-box;
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  -ms-touch-action: pan-y;
  touch-action: pan-y;
  -webkit-tap-highlight-color: transparent;
}

.slick-list {
  position: relative;
  overflow: hidden;
  display: block;
  margin: 0;
  padding: 0;
}

.slick-list:focus {
  outline: none;
}

.slick-list.dragging {
  cursor: pointer;
  cursor: hand;
}

.slick-slider .slick-track,
.slick-slider .slick-list {
  -webkit-transform: translate3d(0, 0, 0);
  -moz-transform: translate3d(0, 0, 0);
  -ms-transform: translate3d(0, 0, 0);
  -o-transform: translate3d(0, 0, 0);
  transform: translate3d(0, 0, 0);
}

.slick-track {
  position: relative;
  left: 0;
  top: 0;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

.slick-track:before,
.slick-track:after {
  content: "";
  display: table;
}

.slick-track:after {
  clear: both;
}

.slick-loading .slick-track {
  visibility: hidden;
}

.slick-slide {
  float: left;
  height: 100%;
  min-height: 1px;
  display: none;
}

[dir="rtl"] .slick-slide {
  float: right;
}

.slick-slide img {
  display: block;
}

.slick-slide.slick-loading img {
  display: none;
}

.slick-slide.dragging img {
  pointer-events: none;
}

.slick-initialized .slick-slide {
  display: block;
}

.slick-loading .slick-slide {
  visibility: hidden;
}

.slick-vertical .slick-slide {
  display: block;
  height: auto;
  border: 1px solid transparent;
}

.slick-arrow.slick-hidden {
  display: none;
}

/* ===================================================================
 * # prettyprint GitHub Theme
 *
 * ------------------------------------------------------------------- */
.prettyprint {
  background: #efefef;
  font-family: Menlo, "Bitstream Vera Sans Mono", "DejaVu Sans Mono", Monaco,
    Consolas, monospace;
  font-size: 13px;
  line-height: 1.538;
  border-radius: 4px;
  border: none;
}

.pln {
  color: #333333;
}

@media screen {
  .str {
    color: #dd1144;
  }

  .kwd {
    color: #333333;
  }

  .com {
    color: #999988;
  }

  .typ {
    color: #445588;
  }

  .lit {
    color: #445588;
  }

  .pun {
    color: #333333;
  }

  .opn {
    color: #333333;
  }

  .clo {
    color: #333333;
  }

  .tag {
    color: navy;
  }

  .atn {
    color: teal;
  }

  .atv {
    color: #dd1144;
  }

  .dec {
    color: #333333;
  }

  .var {
    color: teal;
  }

  .fun {
    color: #990000;
  }
}

@media print, projection {
  .str {
    color: #006600;
  }

  .kwd {
    color: #006;
    font-weight: bold;
  }

  .com {
    color: #600;
    font-style: italic;
  }

  .typ {
    color: #404;
    font-weight: bold;
  }

  .lit {
    color: #004444;
  }

  .pun,
  .opn,
  .clo {
    color: #444400;
  }

  .tag {
    color: #006;
    font-weight: bold;
  }

  .atn {
    color: #440044;
  }

  .atv {
    color: #006600;
  }
}

/* Specify class=linenums on a pre to get line numbering */
ol.linenums {
  margin-top: 0;
  margin-bottom: 0;
}

/* IE indents via margin-left */
li.L0,
li.L1,
li.L2,
li.L3,
li.L4,
li.L5,
li.L6,
li.L7,
li.L8,
li.L9 {
  /* */
}

/* Alternate shading for lines */
li.L1,
li.L3,
li.L5,
li.L7,
li.L9 {
  /* */
}
```
14. On the same folder _Assets_ create the second file called "style__LP.css" and paste the following code inside it:
```css {linenos=table}
/* =================================================================== 
 *  Imminent Main Stylesheet
 *  Template Ver. 1.0.0
 *  09-19-2019
 *  ------------------------------------------------------------------
 *
 *  TOC:
 *  # base style overrides
 *    ## links 
 *  # typography & general theme styles 
 *    ## Lists
 *    ## responsive video container
 *    ## floated image
 *    ## tables
 *    ## Spacing
 *  # preloader
 *  # forms
 *    ## Style Placeholder Text
 *    ## Change Autocomplete styles in Chrome
 *  # buttons
 *  # additional components
 *    ## additional typo styles
 *    ## skillbars
 *    ## alert box
 *  # site header
 *    ## header logo
 *    ## header email 
 *  # intro
 *    ## intro slides
 *    ## intro particles 
 *    ## grid overlay
 *    ## intro content
 *    ## intro content text
 *    ## intro content bottom
 *    ## intro content counter
 *    ## intro content notify
 *    ## modal
 *    ## intro social
 *    ## intro scroll
 *    ## animate intro content
 *    ## intro animations
 *  # info section
 *    ## tabs
 *    ## copyright
 *    ## go top
 *
 * =================================================================== */

/* ===================================================================
 * # base style overrides 
 *
 * ------------------------------------------------------------------- */
html {
  font-size: 10px;
}

@media screen and (max-width: 400px) {
  html {
    font-size: 9.444444444444444px;
  }
}

html,
body {
  height: 100%;
}

body {
  background: #ffffff;
  font-family: "Gothic A1", sans-serif;
  font-size: 1.8rem;
  font-style: normal;
  font-weight: normal;
  line-height: 1.778;
  color: #000000;
  margin: 0;
  padding: 0;
  position: relative;
}

/* ------------------------------------------------------------------- 
 * ## links 
 * ------------------------------------------------------------------- */
a {
  color: rgb(var(--color-base-accent-2));
  transition: all 0.3s cubic-bezier(0.23, 1, 0.32, 1);
}

a:hover,
a:focus,
a:active {
  color: #33648a;
}

a:hover,
a:active {
  outline: 0;
}

/* ===================================================================
 * # typography & general theme styles
 * 
 * ------------------------------------------------------------------- */
h1,
h2,
h3,
h4,
h5,
h6,
.h1,
.h2,
.h3,
.h4,
.h5,
.h6 {
  font-family: "Gothic A1", sans-serif;
  font-weight: 700;
  font-style: normal;
  color: #000000;
  font-variant-ligatures: common-ligatures;
  text-rendering: optimizeLegibility;
}

h1,
.h1,
h2,
.h2,
h3,
.h3,
h4,
.h4 {
  margin-top: 6rem;
  margin-bottom: 1.6rem;
}

@media screen and (max-width: 600px) {
  h1,
  .h1,
  h2,
  .h2,
  h3,
  .h3,
  h4,
  .h4 {
    margin-top: 5.6rem;
  }
}

h5,
.h5,
h6,
.h6 {
  margin-top: 4.8rem;
  margin-bottom: 1.2rem;
}

@media screen and (max-width: 600px) {
  h5,
  .h5,
  h6,
  .h6 {
    margin-top: 4.4rem;
    margin-bottom: 0.8rem;
  }
}

h1,
.h1 {
  font-size: 3.6rem;
  line-height: 1.222;
}

@media screen and (max-width: 600px) {
  h1,
  .h1 {
    font-size: 3.3rem;
  }
}

h2,
.h2 {
  font-size: 3.2rem;
  line-height: 1.25;
}

h3,
.h3 {
  font-size: 2.4rem;
  line-height: 1.167;
}

h4,
.h4 {
  font-size: 2.1rem;
  line-height: 1.333;
}

h5,
.h5 {
  font-size: 1.8rem;
  line-height: 1.333;
}

h6,
.h6 {
  font-size: 1.6rem;
  line-height: 1.5;
  text-transform: uppercase;
  letter-spacing: 0.3rem;
}

p img {
  margin: 0;
}

p.lead {
  font-family: "Gothic A1", sans-serif;
  font-weight: 400;
  font-size: 2.6rem;
  line-height: 1.55;
  margin-bottom: 3.6rem;
  color: #000000;
}

@media screen and (max-width: 1200px) {
  p.lead {
    font-size: 2.4rem;
  }
}

@media screen and (max-width: 600px) {
  p.lead {
    font-size: 2.2rem;
  }
}

em,
i,
strong,
b {
  font-size: inherit;
  line-height: inherit;
}

em,
i {
  font-family: "Gothic A1", sans-serif;
  font-style: italic;
}

strong,
b {
  font-family: "Gothic A1", sans-serif;
  font-weight: 700;
}

small {
  font-size: 1.2rem;
  line-height: inherit;
}

blockquote {
  margin: 4rem 0;
  padding: 4rem 4rem;
  border-left: 4px solid black;
  position: relative;
}

@media screen and (max-width: 600px) {
  blockquote {
    padding: 3.2rem 3.2rem;
  }
}

@media screen and (max-width: 400px) {
  blockquote {
    padding: 2.8rem 2.8rem;
  }
}

blockquote p {
  font-family: "Gothic A1", sans-serif;
  font-weight: 400;
  padding: 0;
  font-size: 2.8rem;
  line-height: 1.857;
  color: #000000;
}

@media screen and (max-width: 1200px) {
  blockquote p {
    font-size: 2.6rem;
  }
}

@media screen and (max-width: 600px) {
  blockquote p {
    font-size: 2.2rem;
  }
}

blockquote cite {
  display: block;
  font-family: "Gothic A1", sans-serif;
  font-size: 1.5rem;
  font-style: normal;
  line-height: 1.333;
}

blockquote cite:before {
  content: "\2014 \0020";
}

blockquote cite,
blockquote cite a,
blockquote cite a:visited {
  color: #646464;
  border: none;
}

abbr {
  font-family: "Gothic A1", sans-serif;
  font-weight: 700;
  font-variant: small-caps;
  text-transform: lowercase;
  letter-spacing: 0.05rem;
  color: #646464;
}

var,
kbd,
samp,
code,
pre {
  font-family: Consolas, "Andale Mono", Courier, "Courier New", monospace;
}

pre {
  padding: 2.4rem 3.2rem 3.2rem;
  background: #efefef;
  overflow-x: auto;
}

code {
  font-size: 1.4rem;
  margin: 0 0.2rem;
  padding: 0.4rem 0.8rem;
  white-space: nowrap;
  background: #efefef;
  border: 1px solid #d3d3d3;
  color: #000000;
  border-radius: 3px;
}

pre > code {
  display: block;
  white-space: pre;
  line-height: 2;
  padding: 0;
  margin: 0;
}

pre.prettyprint > code {
  border: none;
}

del {
  text-decoration: line-through;
}

abbr[title],
dfn[title] {
  border-bottom: 1px dotted;
  cursor: help;
  text-decoration: none;
}

mark {
  background: #fff099;
  color: #000000;
}

hr {
  border: solid #e0e0e0;
  border-width: 1px 0 0;
  clear: both;
  margin: 8rem 0 9.6rem;
  height: 0;
}

/* ------------------------------------------------------------------- 
 * ## Lists 
 * ------------------------------------------------------------------- */
ol {
  list-style: decimal;
}

ul {
  list-style: disc;
}

li {
  display: list-item;
}

ol,
ul {
  margin-left: 1.6rem;
}

ul li {
  padding-left: 0.4rem;
}

ul ul,
ul ol,
ol ol,
ol ul {
  margin: 0.8rem 0 0.8rem 1.6rem;
}

ul.disc li {
  display: list-item;
  list-style: none;
  padding: 0 0 0 0.8rem;
  position: relative;
}

ul.disc li::before {
  content: "";
  display: inline-block;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: rgb(var(--color-base-accent-2));
  position: absolute;
  left: -16px;
  top: 11px;
  vertical-align: middle;
}

dt {
  margin: 0;
  color: rgb(var(--color-base-accent-2));
}

dd {
  margin: 0 0 0 2rem;
}

/* ------------------------------------------------------------------- 
 * ## responsive video container
 * ------------------------------------------------------------------- */
.video-container {
  position: relative;
  padding-bottom: 56.25%;
  height: 0;
  overflow: hidden;
}

.video-container iframe,
.video-container object,
.video-container embed,
.video-container video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

/* ------------------------------------------------------------------- 
 * ## floated image
 * ------------------------------------------------------------------- */
img.h-pull-right {
  margin: 1.2rem 0 1.2rem 2.8rem;
}

img.h-pull-left {
  margin: 1.2rem 2.8rem 1.2rem 0;
}

/* ------------------------------------------------------------------- 
 * ## tables
 * ------------------------------------------------------------------- */
table {
  border-width: 0;
  width: 100%;
  max-width: 100%;
  font-family: "Gothic A1", sans-serif;
  border-collapse: collapse;
}

th,
td {
  padding: 1.5rem 3.2rem;
  text-align: left;
  border-bottom: 1px solid #e0e0e0;
}

th {
  color: #000000;
  font-family: "Gothic A1", sans-serif;
  font-weight: 700;
}

th:first-child,
td:first-child {
  padding-left: 0;
}

th:last-child,
td:last-child {
  padding-right: 0;
}

.table-responsive {
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
}

/* ------------------------------------------------------------------- 
 * ## Spacing
 * ------------------------------------------------------------------- */
button,
.btn {
  margin-bottom: 1.6rem;
}

fieldset {
  margin-bottom: 1.6rem;
}

input,
textarea,
select,
pre,
blockquote,
figure,
table,
p,
ul,
ol,
dl,
form,
.video-container,
.ss-custom-select {
  margin-bottom: 3.2rem;
}

/* ===================================================================
 * # preloader
 *
 * ------------------------------------------------------------------- */
#preloader {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: #1d1d1d;
  z-index: 500;
  height: 100vh;
  width: 100%;
  overflow: hidden;
}

.no-js #preloader,
.oldie #preloader {
  display: none;
}

#loader {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 6px;
  height: 6px;
  padding: 0;
  display: inline-block;
  -webkit-transform: translate3d(-50%, -50%, 0);
  transform: translate3d(-50%, -50%, 0);
}

#loader > div {
  content: "";
  background: #ffffff;
  width: 6px;
  height: 6px;
  position: absolute;
  top: 0;
  left: 0;
  border-radius: 50%;
}

#loader > div:nth-of-type(1) {
  left: 15px;
}

#loader > div:nth-of-type(3) {
  left: -15px;
}

/* dots jump */
.dots-jump > div {
  -webkit-animation: dots-jump 1.2s infinite ease;
  animation: dots-jump 1.2s infinite ease;
  animation-delay: 0.2s;
}

.dots-jump > div:nth-of-type(1) {
  animation-delay: 0.4s;
}

.dots-jump > div:nth-of-type(3) {
  animation-delay: 0s;
}

@-webkit-keyframes dots-jump {
  0% {
    top: 0;
  }

  40% {
    top: -6px;
  }

  80% {
    top: 0;
  }
}

@keyframes dots-jump {
  0% {
    top: 0;
  }

  40% {
    top: -6px;
  }

  80% {
    top: 0;
  }
}

/* dots fade */
.dots-fade > div {
  -webkit-animation: dots-fade 1.6s infinite ease;
  animation: dots-fade 1.6s infinite ease;
  animation-delay: 0.4s;
}

.dots-fade > div:nth-of-type(1) {
  animation-delay: 0.8s;
}

.dots-fade > div:nth-of-type(3) {
  animation-delay: 0s;
}

@-webkit-keyframes dots-fade {
  0% {
    opacity: 1;
  }

  40% {
    opacity: 0.2;
  }

  80% {
    opacity: 1;
  }
}

@keyframes dots-fade {
  0% {
    opacity: 1;
  }

  40% {
    opacity: 0.2;
  }

  80% {
    opacity: 1;
  }
}

/* dots pulse */
.dots-pulse > div {
  -webkit-animation: dots-pulse 1.2s infinite ease;
  animation: dots-pulse 1.2s infinite ease;
  animation-delay: 0.2s;
}

.dots-pulse > div:nth-of-type(1) {
  animation-delay: 0.4s;
}

.dots-pulse > div:nth-of-type(3) {
  animation-delay: 0s;
}

@-webkit-keyframes dots-pulse {
  0% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }

  40% {
    -webkit-transform: scale(1.1);
    transform: scale(1.3);
  }

  80% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }
}

@keyframes dots-pulse {
  0% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }

  40% {
    -webkit-transform: scale(1.1);
    transform: scale(1.3);
  }

  80% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }
}

/* ===================================================================
 * # forms
 *
 * ------------------------------------------------------------------- */
fieldset {
  border: none;
}

input[type="email"],
input[type="number"],
input[type="search"],
input[type="text"],
input[type="tel"],
input[type="url"],
input[type="password"],
textarea,
select {
  display: block;
  height: 6.4rem;
  padding: 1.5rem 24px 1.5rem;
  border: 0;
  outline: none;
  color: #000000;
  font-family: "Gothic A1", sans-serif;
  font-size: 1.5rem;
  line-height: 3.2rem;
  max-width: 100%;
  background-color: #e0e0e0;
  border: 1px solid transparent;
  transition: all 0.3s ease-in-out;
  border-radius: 4px;
}

.ss-custom-select {
  position: relative;
  padding: 0;
}

.ss-custom-select select {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  text-indent: 0.01px;
  text-overflow: "";
  margin: 0;
  line-height: 3rem;
  vertical-align: middle;
}

.ss-custom-select select option {
  padding-left: 2rem;
  padding-right: 2rem;
}

.ss-custom-select select::-ms-expand {
  display: none;
}

.ss-custom-select::after {
  border-bottom: 2px solid #000000;
  border-right: 2px solid #000000;
  content: "";
  display: block;
  height: 8px;
  width: 8px;
  margin-top: -7px;
  pointer-events: none;
  position: absolute;
  right: 2.4rem;
  top: 50%;
  transition: all 0.15s ease-in-out;
  -webkit-transform-origin: 66% 66%;
  transform-origin: 66% 66%;
  -webkit-transform: rotate(45deg);
  transform: rotate(45deg);
}

textarea {
  min-height: 25.6rem;
}

input[type="email"]:focus,
input[type="number"]:focus,
input[type="search"]:focus,
input[type="text"]:focus,
input[type="tel"]:focus,
input[type="url"]:focus,
input[type="password"]:focus,
textarea:focus,
select:focus {
  color: #000000;
  box-shadow: 0 0 5px rgba(var(--color-base-accent-2), 0.8);
  border: 1px solid rgb(var(--color-base-accent-2));
}

label,
legend {
  font-family: "Gothic A1", sans-serif;
  font-weight: 700;
  font-size: 1.4rem;
  line-height: 2;
  margin-bottom: 0.8rem;
  color: #000000;
  display: block;
}

input[type="checkbox"],
input[type="radio"] {
  display: inline;
}

label > .label-text {
  display: inline-block;
  margin-left: 1rem;
  font-family: "Gothic A1", sans-serif;
  line-height: inherit;
}

label > input[type="checkbox"],
label > input[type="radio"] {
  margin: 0;
  position: relative;
  top: 0.2rem;
}

/* ------------------------------------------------------------------- 
 * ## Style Placeholder Text
 * ------------------------------------------------------------------- */
::-webkit-input-placeholder {
  /* WebKit, Blink, Edge */
  color: #8c8c8c;
}

:-moz-placeholder {
  /* Mozilla Firefox 4 to 18 */
  color: #8c8c8c;
  opacity: 1;
}

::-moz-placeholder {
  /* Mozilla Firefox 19+ */
  color: #8c8c8c;
  opacity: 1;
}

:-ms-input-placeholder {
  /* Internet Explorer 10-11 */
  color: #8c8c8c;
}

::-ms-input-placeholder {
  /* Microsoft Edge */
  color: #8c8c8c;
}

::placeholder {
  /* Most modern browsers support this now. */
  color: #8c8c8c;
}

.placeholder {
  color: #8c8c8c !important;
}

/* ------------------------------------------------------------------- 
 * ## Change Autocomplete styles in Chrome
 * ------------------------------------------------------------------- */
input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus input:-webkit-autofill,
textarea:-webkit-autofill,
textarea:-webkit-autofill:hover textarea:-webkit-autofill:focus,
select:-webkit-autofill,
select:-webkit-autofill:hover,
select:-webkit-autofill:focus {
  -webkit-text-fill-color: rgb(var(--color-base-accent-2));
  transition: background-color 5000s ease-in-out 0s;
}

/* ===================================================================
 * # buttons
 *
 * ------------------------------------------------------------------- */
.btn,
button,
input[type="submit"],
input[type="reset"],
input[type="button"] {
  display: inline-block;
  font-family: "Gothic A1", sans-serif;
  font-weight: 700;
  font-size: 1.1rem;
  text-transform: uppercase;
  letter-spacing: 0.6rem;
  height: 6rem;
  line-height: 5.6rem;
  padding: 0 3.2rem;
  margin: 0 0.4rem 1.6rem 0;
  color: #ffffff;
  text-decoration: none;
  text-align: center;
  white-space: nowrap;
  cursor: pointer;
  transition: all 0.3s ease-in-out;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  border-radius: 4px;
  background-color: #272727;
  border: 0.2rem solid #272727;
}

.btn:hover,
button:hover,
input[type="submit"]:hover,
input[type="reset"]:hover,
input[type="button"]:hover,
.btn:focus,
button:focus,
input[type="submit"]:focus,
input[type="reset"]:focus,
input[type="button"]:focus {
  background-color: #000000;
  border-color: #000000;
  color: #ffffff;
  outline: 0;
}

/* button primary
 * ------------------------------------------------- */
.btn.btn--primary,
button.btn--primary,
input[type="submit"].btn--primary,
input[type="reset"].btn--primary,
input[type="button"].btn--primary {
  background: rgb(var(--color-base-accent-2));
  border-color: rgb(var(--color-base-accent-2));
  color: #ffffff;
}

.btn.btn--primary:hover,
button.btn--primary:hover,
input[type="submit"].btn--primary:hover,
input[type="reset"].btn--primary:hover,
input[type="button"].btn--primary:hover,
.btn.btn--primary:focus,
button.btn--primary:focus,
input[type="submit"].btn--primary:focus,
input[type="reset"].btn--primary:focus,
input[type="button"].btn--primary:focus {
  background: #000000;
  border-color: #000000;
}

/* button modifiers
 * ------------------------------------------------- */
.btn.h-full-width,
button.h-full-width {
  width: 100%;
  margin-right: 0;
}

.btn--small,
button.btn--small {
  height: 5.6rem !important;
  line-height: 5.2rem !important;
}

.btn--medium,
button.btn--medium {
  height: 6.4rem !important;
  line-height: 6rem !important;
}

.btn--large,
button.btn--large {
  height: 6.8rem !important;
  line-height: 6.4rem !important;
}

.btn--stroke,
button.btn--stroke {
  background: transparent !important;
  border: 0.2rem solid #000000;
  color: #000000;
}

.btn--stroke:hover,
button.btn--stroke:hover {
  background: #000000 !important;
  border: 0.2rem solid #000000;
  color: #ffffff;
}

.btn--pill,
button.btn--pill {
  padding-left: 3.2rem !important;
  padding-right: 3.2rem !important;
  border-radius: 1000px !important;
}

button::-moz-focus-inner,
input::-moz-focus-inner {
  border: 0;
  padding: 0;
}

/* =================================================================== 
 * # additional components
 *
 * ------------------------------------------------------------------- */

/* ------------------------------------------------------------------- 
 * ## additional typo styles
 * ------------------------------------------------------------------- */
.drop-cap:first-letter {
  float: left;
  font-family: "DM Serif Display", serif;
  font-weight: 400;
  font-size: 5.334em;
  line-height: 1;
  padding: 0 0.125em 0 0;
  text-transform: uppercase;
  background: transparent;
  color: #000000;
}

/* line definition style 
 * ----------------------------------------------- */
.lining dt,
.lining dd {
  display: inline;
  margin: 0;
}

.lining dt + dt:before,
.lining dd + dt:before {
  content: "\A";
  white-space: pre;
}

.lining dd + dd:before {
  content: ", ";
}

.lining dd + dd:before {
  content: ", ";
}

.lining dd:before {
  content: ": ";
  margin-left: -0.2em;
}

/* dictionary definition style 
 * ----------------------------------------------- */
.dictionary-style dt {
  display: inline;
  counter-reset: definitions;
}

.dictionary-style dt + dt:before {
  content: ", ";
  margin-left: -0.2em;
}

.dictionary-style dd {
  display: block;
  counter-increment: definitions;
}

.dictionary-style dd:before {
  content: counter(definitions, decimal) ". ";
}

/** 
 * Pull Quotes
 * -----------
 * markup:
 *
 * <aside class="pull-quote">
 *    <blockquote>
 *      <p></p>
 *    </blockquote>
 *  </aside>
 *
 * --------------------------------------------------------------------- */
.pull-quote {
  position: relative;
  padding: 2.4rem 0;
}

.pull-quote blockquote {
  background-color: #efefef;
  border: none;
  margin: 0;
  padding-top: 9.6rem;
  position: relative;
}

.pull-quote blockquote:before {
  content: "";
  display: block;
  height: 3.2rem;
  width: 3.2rem;
  background-repeat: no-repeat;
  background: center center;
  background-size: contain;
  background-image: url(../images/icons/icon-quote.svg);
  position: absolute;
  top: 4rem;
  left: 4rem;
}

/** 
 * Stats Tab
 * ---------
 * markup:
 *
 * <ul class="stats-tabs">
 *    <li><a href="#">[value]<em>[name]</em></a></li>
 *  </ul>
 *
 * Extend this object into your markup.
 *
 * --------------------------------------------------------------------- */
.stats-tabs {
  padding: 0;
  margin: 3.2rem 0;
}

.stats-tabs li {
  display: inline-block;
  margin: 0 1.6rem 3.2rem 0;
  padding: 0 1.5rem 0 0;
  border-right: 1px solid #e0e0e0;
}

.stats-tabs li:last-child {
  margin: 0;
  padding: 0;
  border: none;
}

.stats-tabs li a {
  display: inline-block;
  font-size: 2.5rem;
  font-family: "Gothic A1", sans-serif;
  font-weight: 700;
  border: none;
  color: #000000;
}

.stats-tabs li a:hover {
  color: rgb(var(--color-base-accent-2));
}

.stats-tabs li a em {
  display: block;
  margin: 0.8rem 0 0 0;
  font-family: "Gothic A1", sans-serif;
  font-size: 1.5rem;
  font-weight: normal;
  font-style: normal;
  color: #646464;
}

/* ------------------------------------------------------------------- 
 * ## skillbars
 * ------------------------------------------------------------------- */
.skill-bars {
  list-style: none;
  margin: 6.8rem 0 3.2rem;
}

.skill-bars li {
  height: 0.4rem;
  background: #c3c3c3;
  width: 100%;
  margin-bottom: 6.8rem;
  padding: 0;
  position: relative;
}

.skill-bars li strong {
  position: absolute;
  left: 0;
  top: -4rem;
  font-family: "Gothic A1", sans-serif;
  font-weight: 700;
  color: #000000;
  text-transform: uppercase;
  letter-spacing: 0.2rem;
  font-size: 1.4rem;
  line-height: 2.4rem;
}

.skill-bars li .progress {
  background: #000000;
  position: relative;
  height: 100%;
}

.skill-bars li .progress span {
  position: absolute;
  right: 0;
  top: -3.6rem;
  display: block;
  font-family: "Gothic A1", sans-serif;
  color: #ffffff;
  font-size: 1.1rem;
  line-height: 1;
  background: #000000;
  padding: 0.8rem 0.8rem;
  border-radius: 3px;
}

.skill-bars li .progress span::after {
  position: absolute;
  left: 50%;
  bottom: -10px;
  margin-left: -5px;
  width: 0;
  height: 0;
  border: 5px solid transparent;
  border-top-color: #000000;
  content: "";
}

.skill-bars li .percent5 {
  width: 5%;
}

.skill-bars li .percent10 {
  width: 10%;
}

.skill-bars li .percent15 {
  width: 15%;
}

.skill-bars li .percent20 {
  width: 20%;
}

.skill-bars li .percent25 {
  width: 25%;
}

.skill-bars li .percent30 {
  width: 30%;
}

.skill-bars li .percent35 {
  width: 35%;
}

.skill-bars li .percent40 {
  width: 40%;
}

.skill-bars li .percent45 {
  width: 45%;
}

.skill-bars li .percent50 {
  width: 50%;
}

.skill-bars li .percent55 {
  width: 55%;
}

.skill-bars li .percent60 {
  width: 60%;
}

.skill-bars li .percent65 {
  width: 65%;
}

.skill-bars li .percent70 {
  width: 70%;
}

.skill-bars li .percent75 {
  width: 75%;
}

.skill-bars li .percent80 {
  width: 80%;
}

.skill-bars li .percent85 {
  width: 85%;
}

.skill-bars li .percent90 {
  width: 90%;
}

.skill-bars li .percent95 {
  width: 95%;
}

.skill-bars li .percent100 {
  width: 100%;
}

/* ------------------------------------------------------------------- 
 * ## alert box
 * ------------------------------------------------------------------- */
.alert-box {
  padding: 2.4rem 4rem 2.4rem 3.2rem;
  position: relative;
  margin-bottom: 3.2rem;
  border-radius: 3px;
  font-family: "DM Sans", sans-serif;
  font-weight: 600;
  font-size: 1.5rem;
  line-height: 1.6;
}

.alert-box__close {
  position: absolute;
  display: block;
  right: 1.6rem;
  top: 1.6rem;
  cursor: pointer;
  width: 12px;
  height: 12px;
}

.alert-box__close::before,
.alert-box__close::after {
  content: "";
  position: absolute;
  display: inline-block;
  width: 2px;
  height: 12px;
  top: 0;
  left: 5px;
}

.alert-box__close::before {
  -webkit-transform: rotate(45deg);
  transform: rotate(45deg);
}

.alert-box__close::after {
  -webkit-transform: rotate(-45deg);
  transform: rotate(-45deg);
}

.alert-box--error {
  background-color: #ffd1d2;
  color: #dd4043;
}

.alert-box--error .alert-box__close::before,
.alert-box--error .alert-box__close::after {
  background-color: #dd4043;
}

.alert-box--success {
  background-color: #c8e675;
  color: #637533;
}

.alert-box--success .alert-box__close::before,
.alert-box--success .alert-box__close::after {
  background-color: #637533;
}

.alert-box--info {
  background-color: #d5ebfb;
  color: #387fb2;
}

.alert-box--info .alert-box__close::before,
.alert-box--info .alert-box__close::after {
  background-color: #387fb2;
}

.alert-box--notice {
  background-color: #fff099;
  color: #827217;
}

.alert-box--notice .alert-box__close::before,
.alert-box--notice .alert-box__close::after {
  background-color: #827217;
}

/* ===================================================================
 * # site header
 *
 * ------------------------------------------------------------------- */
.s-header {
  z-index: 100;
  width: 100%;
  height: 8rem;
  position: absolute;
  top: 4rem;
  left: 0;
}

/* -------------------------------------------------------------------
 * ## header logo
 * ------------------------------------------------------------------- */
.header-logo {
  z-index: 101;
  display: inline-block;
  margin: 0;
  padding: 0;
  transition: all 0.3s;
  -webkit-transform: translate3d(0, -50%, 0);
  transform: translate3d(0, -50%, 0);
  position: absolute;
  left: 8rem;
  top: 50%;
}

.header-logo a {
  display: block;
  padding: 0;
  outline: 0;
  border: none;
}

.header-logo .site-logo__name {
  font-size: 20px;
  color: #fff;
}

/* -------------------------------------------------------------------
 * ## header email
 * ------------------------------------------------------------------- */
.header-email {
  font-size: 1.5rem;
  line-height: 3.2rem;
  -webkit-transform: translate3d(0, -50%, 0);
  transform: translate3d(0, -50%, 0);
  position: absolute;
  top: 50%;
  right: 8rem;
}

.header-email svg {
  fill: #72a130;
  height: 1.5rem;
  width: 1.5rem;
  margin-right: 0.4rem;
  -webkit-transform: translate3d(0, 3px, 0);
  transform: translate3d(0, 3px, 0);
}

.header-email a {
  color: rgba(255, 255, 255, 0.8);
  display: inline-block;
  position: relative;
}

.header-email a::after {
  content: "";
  display: block;
  width: 0;
  height: 1px;
  background-color: #72a130;
  transition: width 0.3s cubic-bezier(0.23, 1, 0.32, 1);
  position: absolute;
  left: 0;
  bottom: 0;
}

.header-email a:hover {
  color: #ffffff;
}

.header-email a:hover::after {
  width: 100%;
}

/* ------------------------------------------------------------------- 
 * responsive:
 * header
 * ------------------------------------------------------------------- */
@media screen and (max-width: 1100px) {
  .header-logo {
    left: 4rem;
  }

  .header-email {
    right: 4rem;
  }
}

@media screen and (max-width: 800px) {
  .s-header {
    top: 1.6rem;
  }

  .header-logo img {
    width: 125px;
    height: 20px;
  }
}

@media screen and (max-width: 600px) {
  .header-logo img {
    width: 120px;
    height: 19px;
  }
}

@media screen and (max-width: 500px) {
  .header-logo {
    left: 3.2rem;
  }

  .header-email {
    right: 3.2rem;
  }
}

@media screen and (max-width: 400px) {
  .header-logo {
    right: auto;
    left: 4.2rem;
  }

  .header-email {
    display: none;
  }
}

/* ===================================================================
 * # intro
 *
 * ------------------------------------------------------------------- */
.s-intro {
  width: 100%;
  height: 100vh;
  /* min-height: 82rem; */
  background-color: #000000;
  overflow: hidden;
  position: relative;
}

.s-intro--static::before {
  display: block;
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #000000;
  opacity: 0.4;
}

.s-intro--static::after {
  display: block;
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(270deg, rgba(0, 0, 0, 0) 0%, black 100%);
  opacity: 0.6;
}

.s-intro--particles {
  background-color: #010e0f;
}

.s-intro--particles::after {
  display: block;
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: transparent;
}

/* -------------------------------------------------------------------
 * ## intro slides
 * ------------------------------------------------------------------- */
.intro-slider {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.intro-slider-img {
  background-repeat: no-repeat;
  background-position: 50% 50%;
  background-size: cover;
  height: 100vh;
  min-height: 82rem;
}

.intro-slider-img::before {
  display: block;
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #000000;
  opacity: 0.5;
}

.intro-slider-img::after {
  display: block;
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(270deg, rgba(0, 0, 0, 0) 0%, black 100%);
  opacity: 0.8;
}

.intro-slider-img.bg-opacity-40::before {
  opacity: 0.4;
}

.intro-slider-img.bg-opacity-50::before {
  opacity: 0.5;
}

.intro-slider-img.bg-opacity-60::before {
  opacity: 0.6;
}

.intro-slider-img.bg-opacity-70::before {
  opacity: 0.7;
}

.intro-slider-img.bg-opacity-80::before {
  opacity: 0.8;
}

.intro-slider-img.bg-opacity-90::before {
  opacity: 0.9;
}

/* -------------------------------------------------------------------
 * ## intro particles 
 * ------------------------------------------------------------------- */
.intro-particles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: transparent;
  padding: 0;
  margin: 0;
  opacity: 0.35;
}

.intro-particles canvas {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

/* -------------------------------------------------------------------
 * ## grid overlay
 * ------------------------------------------------------------------- */
.grid-overlay {
  z-index: 1;
  display: block;
  width: 89%;
  height: 100%;
  max-width: 1200px;
  opacity: 0.65;
  border-right: 1px solid rgba(255, 255, 255, 0.1);
  border-left: 1px solid rgba(255, 255, 255, 0.1);
  -webkit-transform: translate3d(-50%, 0, 0);
  transform: translate3d(-50%, 0, 0);
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 50%;
}

.grid-overlay > div,
.grid-overlay::before,
.grid-overlay::after {
  background-color: rgba(255, 255, 255, 0.1);
  height: 100%;
  width: 1px;
  position: absolute;
  top: 0;
  bottom: 0;
}

.grid-overlay::before {
  content: "";
  left: 25%;
}

.grid-overlay::after {
  content: "";
  right: 25%;
}

.grid-overlay > div {
  left: 50%;
}

/* -------------------------------------------------------------------
 * ## intro content
 * ------------------------------------------------------------------- */
.intro-content {
  z-index: 2;
  height: 100%;
  padding-top: 20vh;
  padding-bottom: 24rem;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  position: relative;
}

/* -------------------------------------------------------------------
 * ## intro content text
 * ------------------------------------------------------------------- */
.intro-content__text h3 {
  display: inline-block;
  font-family: "Gothic A1", sans-serif;
  font-weight: 400;
  font-size: 1.4rem;
  line-height: 2rem;
  text-transform: uppercase;
  letter-spacing: 0.3em;
  color: rgb(var(--color-base-accent-2));
  padding-left: 0.6rem;
  margin-top: 0;
  margin-bottom: 0.8rem;
  position: relative;
}

.intro-content__text h3::before {
  content: "";
  display: block;
  width: 7.2rem;
  height: 1px;
  background-color: rgba(255, 255, 255, 0.15);
  position: absolute;
  top: 1rem;
  right: calc(100% + 2.8rem);
}

.intro-content__text h1 {
  font-family: "DM Serif Display", serif;
  font-weight: 400;
  font-size: 8rem;
  line-height: 1.2;
  color: #ffffff;
  letter-spacing: normal;
  margin-top: 0;
  margin-bottom: 0.8rem;
}

/* -------------------------------------------------------------------
 * ## intro content bottom
 * ------------------------------------------------------------------- */
.intro-content__bottom {
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  -webkit-flex-flow: row wrap;
  -ms-flex-flow: row wrap;
  flex-flow: row wrap;
  -webkit-align-items: flex-end;
  -ms-flex-align: end;
  align-items: flex-end;
  position: absolute;
  left: 20px;
  bottom: 9.6rem;
}

/* -------------------------------------------------------------------
 * ## intro content counter
 * ------------------------------------------------------------------- */
.intro-content__counter-wrap {
  margin-right: 8rem;
}

.intro-content__counter-wrap h4 {
  margin-top: 0;
  margin-bottom: 0.8rem;
  font-family: "Gothic A1", sans-serif;
  font-weight: 400;
  font-size: 1.6rem;
  line-height: 1.25;
  color: rgba(255, 255, 255, 0.8);
}

.counter {
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  -webkit-flex-flow: row wrap;
  -ms-flex-flow: row wrap;
  flex-flow: row wrap;
  font-weight: 600;
  font-size: 3.2rem;
  line-height: 1;
  color: #ffffff;
}

.counter__time {
  margin-top: 1.2rem;
  margin-right: 6px;
}

.counter span {
  font-weight: 400;
  font-size: 1.4rem;
  color: rgba(255, 255, 255, 0.4);
  position: relative;
  left: -2px;
}

/* -------------------------------------------------------------------
 * ## intro content notify
 * ------------------------------------------------------------------- */
.intro-content__notify button {
  z-index: 2;
  font-size: 1rem;
  margin: 0;
  height: 5.6rem !important;
  line-height: 5.4rem !important;
  border: 1px solid #ffffff !important;
  color: #ffffff;
  cursor: pointer;
  overflow: hidden;
  position: relative;
}

.intro-content__notify button svg {
  fill: #ffffff;
  height: 1rem;
  width: 1rem;
  margin-left: 0.4rem;
}

.intro-content__notify button::before {
  z-index: -1;
  content: "";
  height: 100%;
  width: 0;
  background-color: #ffffff;
  transition: all 0.5s cubic-bezier(0.23, 1, 0.32, 1);
  position: absolute;
  top: 0;
  left: 0;
}

.intro-content__notify button:hover {
  color: #000000;
}

.intro-content__notify button:hover svg {
  fill: #000000;
}

.intro-content__notify button:hover::before {
  width: 100%;
}

/* -------------------------------------------------------------------
 * ## modal
 * ------------------------------------------------------------------- */
.modal {
  z-index: 400;
  height: 100%;
  width: 100%;
  font-size: 1.5rem;
  line-height: 1.6;
  text-align: center;
  color: rgba(0, 0, 0, 0.7);
  background-color: rgba(0, 0, 0, 0.8);
  opacity: 0;
  visibility: hidden;
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
  transition: visibility 0s linear 0.3s, opacity 0.3s 0s, transform 0.3s;
  overflow-y: auto;
  position: fixed;
  left: 0;
  top: 0;
}

.modal h3 {
  margin-top: 0;
}

.modal svg {
  fill: rgb(var(--color-base-accent-2));
  width: 4.8rem;
  height: 4.8rem;
}

.modal.show-modal {
  opacity: 1;
  visibility: visible;
  -webkit-transform: scale(1);
  transform: scale(1);
  transition: visibility 0s linear 0s, opacity 0.3s 0s, transform 0.3s;
}

.modal__inner {
  -webkit-transform: translate3d(-50%, -50%, 0);
  transform: translate3d(-50%, -50%, 0);
  padding: 5.6rem 3.2rem 2rem;
  width: 90vw;
  max-width: 34rem;
  border-radius: 0.4rem;
  background-color: #ffffff;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
  position: absolute;
  top: 50%;
  left: 50%;
}

.modal__close {
  display: block;
  right: 2rem;
  top: 2rem;
  cursor: pointer;
  width: 12px;
  height: 12px;
  position: absolute;
}

.modal__close::before,
.modal__close::after {
  content: "";
  position: absolute;
  display: inline-block;
  width: 2px;
  height: 12px;
  top: 0;
  left: 5px;
}

.modal__close::before {
  -webkit-transform: rotate(45deg);
  transform: rotate(45deg);
  background-color: #000000;
}

.modal__close::after {
  -webkit-transform: rotate(-45deg);
  transform: rotate(-45deg);
  background-color: #000000;
}

.modal form input[type="email"] {
  height: 5.6rem;
  padding: 1.2rem 24px 1.2rem;
}

.modal form label {
  font-family: "Gothic A1", sans-serif;
  font-size: 1.3rem;
  line-height: 1.846;
  padding: 0 2rem;
}

.modal form label i {
  padding-right: 6px;
}

.modal form label svg {
  height: 1.3rem !important;
  margin-right: 4px;
}

/* -------------------------------------------------------------------
* ## Form header
* ------------------------------------------------------------------- */
.form__header {
  margin-bottom: 0;
}

.subscribe-message {
  display: flex;
  height: 40px;
  width: 100%;
  background-color: #dff2bf;
  color: #4f8a10;
  justify-content: center;
  align-items: center;
  margin-bottom: 0;
}

/* -------------------------------------------------------------------
 * ## intro social
 * ------------------------------------------------------------------- */
.intro-social {
  z-index: 2;
  list-style: none;
  font-size: 13px;
  line-height: 1.6rem;
  margin: 0;
  padding-bottom: 9.6rem;
  width: 1.5rem;
  text-align: center;
  position: absolute;
  right: 8rem;
  bottom: 0;
}

.intro-social a {
  color: rgba(255, 255, 255, 0.6);
}

.intro-social a:hover,
.intro-social a:focus,
.intro-social a:active {
  color: #ffffff;
}

.intro-social li {
  padding-left: 0;
  margin-bottom: 1.6rem;
}

.intro-social li:last-child {
  margin-bottom: 0;
}

.intro-social::before {
  content: "";
  display: block;
  width: 1px;
  height: 7.8rem;
  background-color: rgba(255, 255, 255, 0.7);
  position: absolute;
  left: 50%;
  bottom: 0;
}

/* -------------------------------------------------------------------
 * ## intro scroll
 * ------------------------------------------------------------------- */
.intro-scroll {
  z-index: 2;
  line-height: 12px;
  position: absolute;
  left: 8rem;
  bottom: 0;
  -webkit-transform: rotate(-90deg) translate3d(0, 100%, 0);
  transform: rotate(-90deg) translate3d(0, 100%, 0);
  -webkit-transform-origin: left bottom;
  transform-origin: left bottom;
}

.intro-scroll .scroll-link {
  font-size: 9px;
  text-transform: uppercase;
  letter-spacing: 4px;
  text-align: left;
  color: rgba(255, 255, 255, 0.8);
  padding-left: 9.6rem;
  margin: 0;
  position: relative;
}

.intro-scroll .scroll-link:hover,
.intro-scroll .scroll-link:focus {
  color: #ffffff;
}

.intro-scroll::before {
  display: block;
  content: "";
  background-color: rgba(255, 255, 255, 0.7);
  width: 7.8rem;
  height: 1px;
  position: absolute;
  left: 0;
  top: 50%;
}

/* -------------------------------------------------------------------
 * ## animate intro content
 * ------------------------------------------------------------------- */
html.ss-preload .intro-content__text,
html.ss-preload .intro-content__bottom {
  opacity: 0;
}

html.ss-loaded .intro-content__text {
  -webkit-animation-name: fadeInLeft;
  animation-name: fadeInLeft;
  -webkit-animation-duration: 3s;
  animation-duration: 3s;
  -webkit-animation-timing-function: cubic-bezier(0.23, 1, 0.32, 1);
  animation-timing-function: cubic-bezier(0.23, 1, 0.32, 1);
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

html.ss-loaded .intro-content__bottom {
  -webkit-animation-name: fadeIn;
  animation-name: fadeIn;
  -webkit-animation-duration: 3s;
  animation-duration: 3s;
  -webkit-animation-timing-function: cubic-bezier(0.23, 1, 0.32, 1);
  animation-timing-function: cubic-bezier(0.23, 1, 0.32, 1);
  -webkit-animation-delay: 1.5s;
  animation-delay: 1.5s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

html.no-csstransitions .intro-content__text,
html.no-csstransitions .intro-content__bottom {
  opacity: 1;
}

/* ------------------------------------------------------------------- 
 * ## intro animations 
 * ------------------------------------------------------------------- */

/* fade in */
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
    visibility: hidden;
    -webkit-transform: translate3d(0, 100%, 0);
    transform: translate3d(0, 100%, 0);
  }

  to {
    opacity: 1;
    visibility: visible;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
    visibility: hidden;
    -webkit-transform: translate3d(0, 100%, 0);
    transform: translate3d(0, 100%, 0);
  }

  to {
    opacity: 1;
    visibility: visible;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

/* fade in left */
@-webkit-keyframes fadeInLeft {
  from {
    opacity: 0;
    visibility: hidden;
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
  }

  to {
    opacity: 1;
    visibility: visible;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

@keyframes fadeInLeft {
  from {
    opacity: 0;
    visibility: hidden;
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
  }

  to {
    opacity: 1;
    visibility: visible;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

/* fade out */
@-webkit-keyframes fadeOut {
  from {
    opacity: 1;
    visibility: visible;
  }

  to {
    opacity: 0;
    visibility: hidden;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
  }
}

@keyframes fadeOut {
  from {
    opacity: 1;
    visibility: visible;
  }

  to {
    opacity: 0;
    visibility: hidden;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
  }
}

/* ------------------------------------------------------------------- 
 * responsive:
 * intro
 * ------------------------------------------------------------------- */
@media screen and (max-width: 1800px) {
  .intro-content__text h1 {
    font-size: 7.3rem;
  }
}

@media screen and (max-width: 1700px) {
  .intro-content {
    max-width: 1200px;
  }
}

@media screen and (max-width: 1600px) {
  .grid-overlay {
    border-right: none !important;
    border-left: none !important;
  }

  .grid-overlay::before {
    left: 22.5%;
  }

  .grid-overlay::after {
    right: 22.5%;
  }

  .intro-content {
    max-width: 1080px;
  }

  .intro-content__text h1 {
    font-size: 7rem;
  }
}

@media screen and (max-width: 1400px) {
  .intro-content {
    max-width: 900px;
  }

  .intro-content__text h1 {
    font-size: 6.6rem;
  }
}

@media screen and (max-width: 1200px) {
  .intro-content {
    max-width: 800px;
  }

  .intro-content__text h1 {
    font-size: 6.3rem;
  }

  .intro-content__bottom {
    left: 16px;
  }
}

@media screen and (max-width: 1100px) {
  .intro-content__text h3::before {
    width: 4rem;
  }

  .intro-social {
    right: 4rem;
  }

  .intro-scroll {
    left: 4rem;
  }
}

@media screen and (max-width: 1024px) {
  .s-intro {
    max-height: 800px;
  }

  .intro-content {
    max-width: 600px;
  }

  .intro-content__text h1 {
    font-size: 6rem;
  }
}

@media screen and (max-width: 800px) {
  .intro-content {
    max-width: 70vw;
    padding-top: 16rem;
  }

  .intro-content__text h3::before {
    display: none;
  }

  .intro-content__text h1 {
    font-size: 4.8rem;
  }

  .intro-content__text br {
    display: none;
  }

  .intro-content__notify {
    margin-top: 3.6rem;
  }
}

@media screen and (max-width: 700px) {
  .intro-content__text h1 {
    font-size: 4.2rem;
  }

  .counter {
    font-size: 2.8rem;
  }

  .counter span {
    font-size: 1.2rem;
  }
}

@media screen and (max-width: 600px) {
  .s-intro {
    max-height: none;
  }

  .intro-content {
    max-width: 80vw;
    padding-bottom: 12rem;
  }

  .intro-content__text h3 {
    font-size: 1.2rem;
  }

  .intro-content__text h1 {
    font-size: 3.8rem;
  }

  .intro-content__bottom {
    left: 10px;
    display: block;
    position: static;
    margin-top: 9.6rem;
  }

  .intro-content__counter-wrap {
    margin-right: 0;
  }
}

@media screen and (max-width: 500px) {
  .intro-content {
    max-width: 90vw;
  }

  .intro-content__bottom {
    margin-right: 5rem;
  }

  .intro-social {
    display: none;
  }

  .intro-scroll {
    -webkit-transform: rotate(-90deg) translate3d(0, 100%, 0);
    transform: translate3d(100%, 0, 0) rotate(-90deg);
    right: 3.2rem;
    left: auto;
  }
}

@media screen and (max-width: 400px) {
  .grid-overlay > div,
  .grid-overlay::before,
  .grid-overlay::after {
    display: none;
  }
}

@media screen and (max-width: 350px) {
  .intro-content__text h1 {
    font-size: 3.4rem;
  }
}

/* ===================================================================
 * # info section
 *
 * ------------------------------------------------------------------- */
.s-info {
  padding-top: 16rem;
  padding-bottom: 8rem;
  background-color: #ffffff;
  position: relative;
}

.s-info .vert-line {
  width: 1.5rem;
  height: 20rem;
  position: absolute;
  top: 0;
  right: 8rem;
}

.s-info .vert-line::before {
  content: "";
  display: block;
  height: inherit;
  width: 1px;
  background-color: rgb(var(--color-base-accent-2));
  position: absolute;
  left: 50%;
  top: 0;
}

.s-info::before {
  display: block;
  content: "";
  width: 55%;
  height: 65%;
  background-color: #ffffff;
  opacity: 0.5;
  background-repeat: no-repeat;
  background-position: right bottom;
  background-size: contain;
  background-image: url(../images/bg-info.jpg);
  position: absolute;
  right: 0;
  bottom: 0;
}

.s-info h2,
.s-info h4 {
  margin-top: 0;
}

.s-info h2 {
  font-family: "DM Serif Display", serif;
  font-weight: 400;
  padding-bottom: 3.6rem;
  margin-bottom: 3.6rem;
  position: relative;
}

.s-info h2::after {
  display: block;
  content: "";
  width: 8rem;
  height: 1px;
  background-color: rgb(var(--color-base-accent-2));
  position: absolute;
  left: 0;
  bottom: 0;
}

.s-info footer {
  margin-top: 9.6rem;
}

/* -------------------------------------------------------------------
 * ## tabs
 * ------------------------------------------------------------------- */

/* tabs navigation
 * -------------------------------------- */
.tab-nav {
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
}

.tab-nav__list {
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  list-style: none;
  margin: 0;
  font-size: 1.6rem;
  line-height: 6.8rem;
  position: relative;
}

.tab-nav__list li {
  -webkit-flex-shrink: 0;
  -ms-flex-shrink: 0;
  flex-shrink: 0;
  padding: 0;
  border-bottom: 1px solid #efefef;
}

.tab-nav__list a {
  display: block;
  color: rgba(0, 0, 0, 0.5);
  padding: 0 3.2rem;
  position: relative;
}

.tab-nav__list a:hover,
.tab-nav__list a:focus,
.tab-nav__list a:active {
  color: #000000;
}

.tab-nav__list .active a {
  color: #000000;
  background-color: #efefef;
  border-radius: 4px 4px 0 0;
  position: relative;
}

/* tab content
 * -------------------------------------- */
.tab-content {
  margin-top: 6.4rem;
  padding-right: 25vw;
  position: relative;
}

/* services listing
 * --------------------------------------- */
.services-list {
  margin-top: 4rem;
  counter-reset: ctr;
  position: relative;
}

.services-list__item {
  margin-bottom: 2.4rem;
}

.services-list__item-content::before {
  display: block;
  content: counter(ctr, decimal-leading-zero) ".";
  counter-increment: ctr;
  margin-bottom: 2rem;
  font-family: "Gothic A1", sans-serif;
  font-weight: 700;
  font-size: 3.6rem;
  line-height: 1;
  color: rgb(var(--color-base-accent-2));
}

/* link list
 * -------------------------------------- */
.link-list {
  list-style: none;
  margin-left: 0;
}

.link-list li {
  padding-left: 0;
}

.link-list a {
  color: #000000;
}

.link-list a:hover,
.link-list a:focus,
.link-list a:active {
  color: rgb(var(--color-base-accent-2));
}

/* tab contact bottom
 * -------------------------------------- */
.contact-email {
  display: inline-block;
  font-family: "Gothic A1", sans-serif;
  font-size: 6rem;
  font-weight: 700;
  line-height: 1;
  margin: 5.6rem 0 0.8rem;
  color: rgb(var(--color-base-accent-2));
  border-bottom: 1px solid #efefef;
}

.contact-email:hover,
.contact-email:focus {
  color: rgb(var(--color-base-accent-2));
  border-bottom: 1px solid rgba(0, 0, 0, 0.5);
}

.contact-number {
  display: block;
  font-size: 2rem;
  font-weight: 700;
  line-height: 1.8;
}

.contact-number a {
  color: #000000;
}

.contact-number a:hover,
.contact-number a:focus {
  color: rgb(var(--color-base-accent-2));
}

.contact-number a::after {
  content: "/";
  font-weight: 400;
  margin: 0 0.6rem 0 1rem;
  color: #646464;
}

.contact-number a:last-child::after {
  display: none;
}

/* ------------------------------------------------------------------- 
 * ## copyright
 * ------------------------------------------------------------------- */
.ss-copyright {
  z-index: 2;
  position: relative;
}

.ss-copyright span {
  font-size: 1.5rem;
  display: inline-block;
}

.ss-copyright span::after {
  content: "|";
  display: inline-block;
  padding: 0 0.8rem 0 1rem;
  color: rgba(0, 0, 0, 0.3);
}

.ss-copyright span:last-child::after {
  display: none;
}

/* ------------------------------------------------------------------- 
 * ## go top
 * ------------------------------------------------------------------- */
.ss-go-top {
  z-index: 2;
  position: absolute;
  bottom: 7.2rem;
  right: 6.4rem;
}

.ss-go-top a {
  text-decoration: none;
  border: 0 none;
  display: block;
  height: 5.6rem;
  width: 5.6rem;
  line-height: 5.6rem;
  text-align: center;
  background: black;
  color: black;
  border-radius: 50%;
  transition: all 0.3s;
  position: relative;
}

.ss-go-top a:hover {
  background-color: #254965;
  color: #ffffff;
}

.ss-go-top svg {
  height: 1.2rem;
  width: 1.2rem;
  fill: #ffffff;
  -webkit-transform: translate3d(-50%, -50%, 0);
  transform: translate3d(-50%, -50%, 0);
  position: absolute;
  top: 50%;
  left: 50%;
}

/* ------------------------------------------------------------------- 
 * responsive:
 * info
 * ------------------------------------------------------------------- */
@media screen and (max-width: 1200px) {
  .tab-content {
    padding-right: 15vw;
  }
}

@media screen and (max-width: 1100px) {
  .s-info .vert-line {
    right: 4rem;
  }
}

@media screen and (max-width: 1000px) {
  .tab-content {
    padding-right: 40px;
  }
}

@media screen and (max-width: 800px) {
  .tab-content {
    padding-right: 0;
  }

  .services-list__item-content {
    padding-right: 60px;
  }

  .contact-email {
    font-size: 5.8vw;
  }

  .ss-copyright span {
    display: block;
  }

  .ss-copyright span::after {
    display: none;
  }

  .ss-go-top {
    right: 4rem;
  }
}

@media screen and (max-width: 600px) {
  .s-info {
    padding-top: 12rem;
  }

  .tab-nav__list {
    font-size: 1.5rem;
    line-height: 5.6rem;
  }

  .tab-nav__list a {
    padding: 0 2.2rem;
  }

  .services-list__item-content {
    padding-right: 0;
  }
}

@media screen and (max-width: 500px) {
  .s-info {
    padding-top: 9.6rem;
  }

  .s-info .vert-line {
    display: none;
  }

  .ss-go-top {
    bottom: 8rem;
  }

  .ss-go-top a {
    height: 4.8rem;
    width: 4.8rem;
    line-height: 4.8rem;
  }
}

@media screen and (max-width: 400px) {
  .s-info footer {
    text-align: center;
    position: relative;
    margin-top: 4.8rem;
    padding-top: 6.4rem;
  }

  .services-list__item-content::before {
    font-size: 3.3rem;
  }

  .ss-go-top {
    right: 50%;
    top: 0;
    bottom: auto;
    -webkit-transform: translate3d(50%, 0, 0);
    transform: translate3d(50%, 0, 0);
  }
}
```
15. Again in the _Assets_ folder create the third file called "plugins__LP.min.js" and paste the following code in it:
```js {linenos=table}
/** 
 * ===================================================================
 * javascript plugins
 *
 * ------------------------------------------------------------------- 
 */


/*
     _ _      _       _
 ___| (_) ___| | __  (_)___
/ __| | |/ __| |/ /  | / __|
\__ \ | | (__|   < _ | \__ \
|___/_|_|\___|_|\_(_)/ |___/
                   |__/

 Version: 1.8.0
  Author: Ken Wheeler
 Website: http://kenwheeler.github.io
    Docs: http://kenwheeler.github.io/slick
    Repo: http://github.com/kenwheeler/slick
  Issues: http://github.com/kenwheeler/slick/issues

 */
!function(i){"use strict";"function"==typeof define&&define.amd?define(["jquery"],i):"undefined"!=typeof exports?module.exports=i(require("jquery")):i(jQuery)}(function(i){"use strict";var e=window.Slick||{};(e=function(){var e=0;return function(t,o){var s,n=this;n.defaults={accessibility:!0,adaptiveHeight:!1,appendArrows:i(t),appendDots:i(t),arrows:!0,asNavFor:null,prevArrow:'<button class="slick-prev" aria-label="Previous" type="button">Previous</button>',nextArrow:'<button class="slick-next" aria-label="Next" type="button">Next</button>',autoplay:!1,autoplaySpeed:3e3,centerMode:!1,centerPadding:"50px",cssEase:"ease",customPaging:function(e,t){return i('<button type="button" />').text(t+1)},dots:!1,dotsClass:"slick-dots",draggable:!0,easing:"linear",edgeFriction:.35,fade:!1,focusOnSelect:!1,focusOnChange:!1,infinite:!0,initialSlide:0,lazyLoad:"ondemand",mobileFirst:!1,pauseOnHover:!0,pauseOnFocus:!0,pauseOnDotsHover:!1,respondTo:"window",responsive:null,rows:1,rtl:!1,slide:"",slidesPerRow:1,slidesToShow:1,slidesToScroll:1,speed:500,swipe:!0,swipeToSlide:!1,touchMove:!0,touchThreshold:5,useCSS:!0,useTransform:!0,variableWidth:!1,vertical:!1,verticalSwiping:!1,waitForAnimate:!0,zIndex:1e3},n.initials={animating:!1,dragging:!1,autoPlayTimer:null,currentDirection:0,currentLeft:null,currentSlide:0,direction:1,$dots:null,listWidth:null,listHeight:null,loadIndex:0,$nextArrow:null,$prevArrow:null,scrolling:!1,slideCount:null,slideWidth:null,$slideTrack:null,$slides:null,sliding:!1,slideOffset:0,swipeLeft:null,swiping:!1,$list:null,touchObject:{},transformsEnabled:!1,unslicked:!1},i.extend(n,n.initials),n.activeBreakpoint=null,n.animType=null,n.animProp=null,n.breakpoints=[],n.breakpointSettings=[],n.cssTransitions=!1,n.focussed=!1,n.interrupted=!1,n.hidden="hidden",n.paused=!0,n.positionProp=null,n.respondTo=null,n.rowCount=1,n.shouldClick=!0,n.$slider=i(t),n.$slidesCache=null,n.transformType=null,n.transitionType=null,n.visibilityChange="visibilitychange",n.windowWidth=0,n.windowTimer=null,s=i(t).data("slick")||{},n.options=i.extend({},n.defaults,o,s),n.currentSlide=n.options.initialSlide,n.originalSettings=n.options,void 0!==document.mozHidden?(n.hidden="mozHidden",n.visibilityChange="mozvisibilitychange"):void 0!==document.webkitHidden&&(n.hidden="webkitHidden",n.visibilityChange="webkitvisibilitychange"),n.autoPlay=i.proxy(n.autoPlay,n),n.autoPlayClear=i.proxy(n.autoPlayClear,n),n.autoPlayIterator=i.proxy(n.autoPlayIterator,n),n.changeSlide=i.proxy(n.changeSlide,n),n.clickHandler=i.proxy(n.clickHandler,n),n.selectHandler=i.proxy(n.selectHandler,n),n.setPosition=i.proxy(n.setPosition,n),n.swipeHandler=i.proxy(n.swipeHandler,n),n.dragHandler=i.proxy(n.dragHandler,n),n.keyHandler=i.proxy(n.keyHandler,n),n.instanceUid=e++,n.htmlExpr=/^(?:\s*(<[\w\W]+>)[^>]*)$/,n.registerBreakpoints(),n.init(!0)}}()).prototype.activateADA=function(){this.$slideTrack.find(".slick-active").attr({"aria-hidden":"false"}).find("a, input, button, select").attr({tabindex:"0"})},e.prototype.addSlide=e.prototype.slickAdd=function(e,t,o){var s=this;if("boolean"==typeof t)o=t,t=null;else if(t<0||t>=s.slideCount)return!1;s.unload(),"number"==typeof t?0===t&&0===s.$slides.length?i(e).appendTo(s.$slideTrack):o?i(e).insertBefore(s.$slides.eq(t)):i(e).insertAfter(s.$slides.eq(t)):!0===o?i(e).prependTo(s.$slideTrack):i(e).appendTo(s.$slideTrack),s.$slides=s.$slideTrack.children(this.options.slide),s.$slideTrack.children(this.options.slide).detach(),s.$slideTrack.append(s.$slides),s.$slides.each(function(e,t){i(t).attr("data-slick-index",e)}),s.$slidesCache=s.$slides,s.reinit()},e.prototype.animateHeight=function(){var i=this;if(1===i.options.slidesToShow&&!0===i.options.adaptiveHeight&&!1===i.options.vertical){var e=i.$slides.eq(i.currentSlide).outerHeight(!0);i.$list.animate({height:e},i.options.speed)}},e.prototype.animateSlide=function(e,t){var o={},s=this;s.animateHeight(),!0===s.options.rtl&&!1===s.options.vertical&&(e=-e),!1===s.transformsEnabled?!1===s.options.vertical?s.$slideTrack.animate({left:e},s.options.speed,s.options.easing,t):s.$slideTrack.animate({top:e},s.options.speed,s.options.easing,t):!1===s.cssTransitions?(!0===s.options.rtl&&(s.currentLeft=-s.currentLeft),i({animStart:s.currentLeft}).animate({animStart:e},{duration:s.options.speed,easing:s.options.easing,step:function(i){i=Math.ceil(i),!1===s.options.vertical?(o[s.animType]="translate("+i+"px, 0px)",s.$slideTrack.css(o)):(o[s.animType]="translate(0px,"+i+"px)",s.$slideTrack.css(o))},complete:function(){t&&t.call()}})):(s.applyTransition(),e=Math.ceil(e),!1===s.options.vertical?o[s.animType]="translate3d("+e+"px, 0px, 0px)":o[s.animType]="translate3d(0px,"+e+"px, 0px)",s.$slideTrack.css(o),t&&setTimeout(function(){s.disableTransition(),t.call()},s.options.speed))},e.prototype.getNavTarget=function(){var e=this,t=e.options.asNavFor;return t&&null!==t&&(t=i(t).not(e.$slider)),t},e.prototype.asNavFor=function(e){var t=this.getNavTarget();null!==t&&"object"==typeof t&&t.each(function(){var t=i(this).slick("getSlick");t.unslicked||t.slideHandler(e,!0)})},e.prototype.applyTransition=function(i){var e=this,t={};!1===e.options.fade?t[e.transitionType]=e.transformType+" "+e.options.speed+"ms "+e.options.cssEase:t[e.transitionType]="opacity "+e.options.speed+"ms "+e.options.cssEase,!1===e.options.fade?e.$slideTrack.css(t):e.$slides.eq(i).css(t)},e.prototype.autoPlay=function(){var i=this;i.autoPlayClear(),i.slideCount>i.options.slidesToShow&&(i.autoPlayTimer=setInterval(i.autoPlayIterator,i.options.autoplaySpeed))},e.prototype.autoPlayClear=function(){var i=this;i.autoPlayTimer&&clearInterval(i.autoPlayTimer)},e.prototype.autoPlayIterator=function(){var i=this,e=i.currentSlide+i.options.slidesToScroll;i.paused||i.interrupted||i.focussed||(!1===i.options.infinite&&(1===i.direction&&i.currentSlide+1===i.slideCount-1?i.direction=0:0===i.direction&&(e=i.currentSlide-i.options.slidesToScroll,i.currentSlide-1==0&&(i.direction=1))),i.slideHandler(e))},e.prototype.buildArrows=function(){var e=this;!0===e.options.arrows&&(e.$prevArrow=i(e.options.prevArrow).addClass("slick-arrow"),e.$nextArrow=i(e.options.nextArrow).addClass("slick-arrow"),e.slideCount>e.options.slidesToShow?(e.$prevArrow.removeClass("slick-hidden").removeAttr("aria-hidden tabindex"),e.$nextArrow.removeClass("slick-hidden").removeAttr("aria-hidden tabindex"),e.htmlExpr.test(e.options.prevArrow)&&e.$prevArrow.prependTo(e.options.appendArrows),e.htmlExpr.test(e.options.nextArrow)&&e.$nextArrow.appendTo(e.options.appendArrows),!0!==e.options.infinite&&e.$prevArrow.addClass("slick-disabled").attr("aria-disabled","true")):e.$prevArrow.add(e.$nextArrow).addClass("slick-hidden").attr({"aria-disabled":"true",tabindex:"-1"}))},e.prototype.buildDots=function(){var e,t,o=this;if(!0===o.options.dots){for(o.$slider.addClass("slick-dotted"),t=i("<ul />").addClass(o.options.dotsClass),e=0;e<=o.getDotCount();e+=1)t.append(i("<li />").append(o.options.customPaging.call(this,o,e)));o.$dots=t.appendTo(o.options.appendDots),o.$dots.find("li").first().addClass("slick-active")}},e.prototype.buildOut=function(){var e=this;e.$slides=e.$slider.children(e.options.slide+":not(.slick-cloned)").addClass("slick-slide"),e.slideCount=e.$slides.length,e.$slides.each(function(e,t){i(t).attr("data-slick-index",e).data("originalStyling",i(t).attr("style")||"")}),e.$slider.addClass("slick-slider"),e.$slideTrack=0===e.slideCount?i('<div class="slick-track"/>').appendTo(e.$slider):e.$slides.wrapAll('<div class="slick-track"/>').parent(),e.$list=e.$slideTrack.wrap('<div class="slick-list"/>').parent(),e.$slideTrack.css("opacity",0),!0!==e.options.centerMode&&!0!==e.options.swipeToSlide||(e.options.slidesToScroll=1),i("img[data-lazy]",e.$slider).not("[src]").addClass("slick-loading"),e.setupInfinite(),e.buildArrows(),e.buildDots(),e.updateDots(),e.setSlideClasses("number"==typeof e.currentSlide?e.currentSlide:0),!0===e.options.draggable&&e.$list.addClass("draggable")},e.prototype.buildRows=function(){var i,e,t,o,s,n,r,l=this;if(o=document.createDocumentFragment(),n=l.$slider.children(),l.options.rows>1){for(r=l.options.slidesPerRow*l.options.rows,s=Math.ceil(n.length/r),i=0;i<s;i++){var d=document.createElement("div");for(e=0;e<l.options.rows;e++){var a=document.createElement("div");for(t=0;t<l.options.slidesPerRow;t++){var c=i*r+(e*l.options.slidesPerRow+t);n.get(c)&&a.appendChild(n.get(c))}d.appendChild(a)}o.appendChild(d)}l.$slider.empty().append(o),l.$slider.children().children().children().css({width:100/l.options.slidesPerRow+"%",display:"inline-block"})}},e.prototype.checkResponsive=function(e,t){var o,s,n,r=this,l=!1,d=r.$slider.width(),a=window.innerWidth||i(window).width();if("window"===r.respondTo?n=a:"slider"===r.respondTo?n=d:"min"===r.respondTo&&(n=Math.min(a,d)),r.options.responsive&&r.options.responsive.length&&null!==r.options.responsive){s=null;for(o in r.breakpoints)r.breakpoints.hasOwnProperty(o)&&(!1===r.originalSettings.mobileFirst?n<r.breakpoints[o]&&(s=r.breakpoints[o]):n>r.breakpoints[o]&&(s=r.breakpoints[o]));null!==s?null!==r.activeBreakpoint?(s!==r.activeBreakpoint||t)&&(r.activeBreakpoint=s,"unslick"===r.breakpointSettings[s]?r.unslick(s):(r.options=i.extend({},r.originalSettings,r.breakpointSettings[s]),!0===e&&(r.currentSlide=r.options.initialSlide),r.refresh(e)),l=s):(r.activeBreakpoint=s,"unslick"===r.breakpointSettings[s]?r.unslick(s):(r.options=i.extend({},r.originalSettings,r.breakpointSettings[s]),!0===e&&(r.currentSlide=r.options.initialSlide),r.refresh(e)),l=s):null!==r.activeBreakpoint&&(r.activeBreakpoint=null,r.options=r.originalSettings,!0===e&&(r.currentSlide=r.options.initialSlide),r.refresh(e),l=s),e||!1===l||r.$slider.trigger("breakpoint",[r,l])}},e.prototype.changeSlide=function(e,t){var o,s,n,r=this,l=i(e.currentTarget);switch(l.is("a")&&e.preventDefault(),l.is("li")||(l=l.closest("li")),n=r.slideCount%r.options.slidesToScroll!=0,o=n?0:(r.slideCount-r.currentSlide)%r.options.slidesToScroll,e.data.message){case"previous":s=0===o?r.options.slidesToScroll:r.options.slidesToShow-o,r.slideCount>r.options.slidesToShow&&r.slideHandler(r.currentSlide-s,!1,t);break;case"next":s=0===o?r.options.slidesToScroll:o,r.slideCount>r.options.slidesToShow&&r.slideHandler(r.currentSlide+s,!1,t);break;case"index":var d=0===e.data.index?0:e.data.index||l.index()*r.options.slidesToScroll;r.slideHandler(r.checkNavigable(d),!1,t),l.children().trigger("focus");break;default:return}},e.prototype.checkNavigable=function(i){var e,t;if(e=this.getNavigableIndexes(),t=0,i>e[e.length-1])i=e[e.length-1];else for(var o in e){if(i<e[o]){i=t;break}t=e[o]}return i},e.prototype.cleanUpEvents=function(){var e=this;e.options.dots&&null!==e.$dots&&(i("li",e.$dots).off("click.slick",e.changeSlide).off("mouseenter.slick",i.proxy(e.interrupt,e,!0)).off("mouseleave.slick",i.proxy(e.interrupt,e,!1)),!0===e.options.accessibility&&e.$dots.off("keydown.slick",e.keyHandler)),e.$slider.off("focus.slick blur.slick"),!0===e.options.arrows&&e.slideCount>e.options.slidesToShow&&(e.$prevArrow&&e.$prevArrow.off("click.slick",e.changeSlide),e.$nextArrow&&e.$nextArrow.off("click.slick",e.changeSlide),!0===e.options.accessibility&&(e.$prevArrow&&e.$prevArrow.off("keydown.slick",e.keyHandler),e.$nextArrow&&e.$nextArrow.off("keydown.slick",e.keyHandler))),e.$list.off("touchstart.slick mousedown.slick",e.swipeHandler),e.$list.off("touchmove.slick mousemove.slick",e.swipeHandler),e.$list.off("touchend.slick mouseup.slick",e.swipeHandler),e.$list.off("touchcancel.slick mouseleave.slick",e.swipeHandler),e.$list.off("click.slick",e.clickHandler),i(document).off(e.visibilityChange,e.visibility),e.cleanUpSlideEvents(),!0===e.options.accessibility&&e.$list.off("keydown.slick",e.keyHandler),!0===e.options.focusOnSelect&&i(e.$slideTrack).children().off("click.slick",e.selectHandler),i(window).off("orientationchange.slick.slick-"+e.instanceUid,e.orientationChange),i(window).off("resize.slick.slick-"+e.instanceUid,e.resize),i("[draggable!=true]",e.$slideTrack).off("dragstart",e.preventDefault),i(window).off("load.slick.slick-"+e.instanceUid,e.setPosition)},e.prototype.cleanUpSlideEvents=function(){var e=this;e.$list.off("mouseenter.slick",i.proxy(e.interrupt,e,!0)),e.$list.off("mouseleave.slick",i.proxy(e.interrupt,e,!1))},e.prototype.cleanUpRows=function(){var i,e=this;e.options.rows>1&&((i=e.$slides.children().children()).removeAttr("style"),e.$slider.empty().append(i))},e.prototype.clickHandler=function(i){!1===this.shouldClick&&(i.stopImmediatePropagation(),i.stopPropagation(),i.preventDefault())},e.prototype.destroy=function(e){var t=this;t.autoPlayClear(),t.touchObject={},t.cleanUpEvents(),i(".slick-cloned",t.$slider).detach(),t.$dots&&t.$dots.remove(),t.$prevArrow&&t.$prevArrow.length&&(t.$prevArrow.removeClass("slick-disabled slick-arrow slick-hidden").removeAttr("aria-hidden aria-disabled tabindex").css("display",""),t.htmlExpr.test(t.options.prevArrow)&&t.$prevArrow.remove()),t.$nextArrow&&t.$nextArrow.length&&(t.$nextArrow.removeClass("slick-disabled slick-arrow slick-hidden").removeAttr("aria-hidden aria-disabled tabindex").css("display",""),t.htmlExpr.test(t.options.nextArrow)&&t.$nextArrow.remove()),t.$slides&&(t.$slides.removeClass("slick-slide slick-active slick-center slick-visible slick-current").removeAttr("aria-hidden").removeAttr("data-slick-index").each(function(){i(this).attr("style",i(this).data("originalStyling"))}),t.$slideTrack.children(this.options.slide).detach(),t.$slideTrack.detach(),t.$list.detach(),t.$slider.append(t.$slides)),t.cleanUpRows(),t.$slider.removeClass("slick-slider"),t.$slider.removeClass("slick-initialized"),t.$slider.removeClass("slick-dotted"),t.unslicked=!0,e||t.$slider.trigger("destroy",[t])},e.prototype.disableTransition=function(i){var e=this,t={};t[e.transitionType]="",!1===e.options.fade?e.$slideTrack.css(t):e.$slides.eq(i).css(t)},e.prototype.fadeSlide=function(i,e){var t=this;!1===t.cssTransitions?(t.$slides.eq(i).css({zIndex:t.options.zIndex}),t.$slides.eq(i).animate({opacity:1},t.options.speed,t.options.easing,e)):(t.applyTransition(i),t.$slides.eq(i).css({opacity:1,zIndex:t.options.zIndex}),e&&setTimeout(function(){t.disableTransition(i),e.call()},t.options.speed))},e.prototype.fadeSlideOut=function(i){var e=this;!1===e.cssTransitions?e.$slides.eq(i).animate({opacity:0,zIndex:e.options.zIndex-2},e.options.speed,e.options.easing):(e.applyTransition(i),e.$slides.eq(i).css({opacity:0,zIndex:e.options.zIndex-2}))},e.prototype.filterSlides=e.prototype.slickFilter=function(i){var e=this;null!==i&&(e.$slidesCache=e.$slides,e.unload(),e.$slideTrack.children(this.options.slide).detach(),e.$slidesCache.filter(i).appendTo(e.$slideTrack),e.reinit())},e.prototype.focusHandler=function(){var e=this;e.$slider.off("focus.slick blur.slick").on("focus.slick blur.slick","*",function(t){t.stopImmediatePropagation();var o=i(this);setTimeout(function(){e.options.pauseOnFocus&&(e.focussed=o.is(":focus"),e.autoPlay())},0)})},e.prototype.getCurrent=e.prototype.slickCurrentSlide=function(){return this.currentSlide},e.prototype.getDotCount=function(){var i=this,e=0,t=0,o=0;if(!0===i.options.infinite)if(i.slideCount<=i.options.slidesToShow)++o;else for(;e<i.slideCount;)++o,e=t+i.options.slidesToScroll,t+=i.options.slidesToScroll<=i.options.slidesToShow?i.options.slidesToScroll:i.options.slidesToShow;else if(!0===i.options.centerMode)o=i.slideCount;else if(i.options.asNavFor)for(;e<i.slideCount;)++o,e=t+i.options.slidesToScroll,t+=i.options.slidesToScroll<=i.options.slidesToShow?i.options.slidesToScroll:i.options.slidesToShow;else o=1+Math.ceil((i.slideCount-i.options.slidesToShow)/i.options.slidesToScroll);return o-1},e.prototype.getLeft=function(i){var e,t,o,s,n=this,r=0;return n.slideOffset=0,t=n.$slides.first().outerHeight(!0),!0===n.options.infinite?(n.slideCount>n.options.slidesToShow&&(n.slideOffset=n.slideWidth*n.options.slidesToShow*-1,s=-1,!0===n.options.vertical&&!0===n.options.centerMode&&(2===n.options.slidesToShow?s=-1.5:1===n.options.slidesToShow&&(s=-2)),r=t*n.options.slidesToShow*s),n.slideCount%n.options.slidesToScroll!=0&&i+n.options.slidesToScroll>n.slideCount&&n.slideCount>n.options.slidesToShow&&(i>n.slideCount?(n.slideOffset=(n.options.slidesToShow-(i-n.slideCount))*n.slideWidth*-1,r=(n.options.slidesToShow-(i-n.slideCount))*t*-1):(n.slideOffset=n.slideCount%n.options.slidesToScroll*n.slideWidth*-1,r=n.slideCount%n.options.slidesToScroll*t*-1))):i+n.options.slidesToShow>n.slideCount&&(n.slideOffset=(i+n.options.slidesToShow-n.slideCount)*n.slideWidth,r=(i+n.options.slidesToShow-n.slideCount)*t),n.slideCount<=n.options.slidesToShow&&(n.slideOffset=0,r=0),!0===n.options.centerMode&&n.slideCount<=n.options.slidesToShow?n.slideOffset=n.slideWidth*Math.floor(n.options.slidesToShow)/2-n.slideWidth*n.slideCount/2:!0===n.options.centerMode&&!0===n.options.infinite?n.slideOffset+=n.slideWidth*Math.floor(n.options.slidesToShow/2)-n.slideWidth:!0===n.options.centerMode&&(n.slideOffset=0,n.slideOffset+=n.slideWidth*Math.floor(n.options.slidesToShow/2)),e=!1===n.options.vertical?i*n.slideWidth*-1+n.slideOffset:i*t*-1+r,!0===n.options.variableWidth&&(o=n.slideCount<=n.options.slidesToShow||!1===n.options.infinite?n.$slideTrack.children(".slick-slide").eq(i):n.$slideTrack.children(".slick-slide").eq(i+n.options.slidesToShow),e=!0===n.options.rtl?o[0]?-1*(n.$slideTrack.width()-o[0].offsetLeft-o.width()):0:o[0]?-1*o[0].offsetLeft:0,!0===n.options.centerMode&&(o=n.slideCount<=n.options.slidesToShow||!1===n.options.infinite?n.$slideTrack.children(".slick-slide").eq(i):n.$slideTrack.children(".slick-slide").eq(i+n.options.slidesToShow+1),e=!0===n.options.rtl?o[0]?-1*(n.$slideTrack.width()-o[0].offsetLeft-o.width()):0:o[0]?-1*o[0].offsetLeft:0,e+=(n.$list.width()-o.outerWidth())/2)),e},e.prototype.getOption=e.prototype.slickGetOption=function(i){return this.options[i]},e.prototype.getNavigableIndexes=function(){var i,e=this,t=0,o=0,s=[];for(!1===e.options.infinite?i=e.slideCount:(t=-1*e.options.slidesToScroll,o=-1*e.options.slidesToScroll,i=2*e.slideCount);t<i;)s.push(t),t=o+e.options.slidesToScroll,o+=e.options.slidesToScroll<=e.options.slidesToShow?e.options.slidesToScroll:e.options.slidesToShow;return s},e.prototype.getSlick=function(){return this},e.prototype.getSlideCount=function(){var e,t,o=this;return t=!0===o.options.centerMode?o.slideWidth*Math.floor(o.options.slidesToShow/2):0,!0===o.options.swipeToSlide?(o.$slideTrack.find(".slick-slide").each(function(s,n){if(n.offsetLeft-t+i(n).outerWidth()/2>-1*o.swipeLeft)return e=n,!1}),Math.abs(i(e).attr("data-slick-index")-o.currentSlide)||1):o.options.slidesToScroll},e.prototype.goTo=e.prototype.slickGoTo=function(i,e){this.changeSlide({data:{message:"index",index:parseInt(i)}},e)},e.prototype.init=function(e){var t=this;i(t.$slider).hasClass("slick-initialized")||(i(t.$slider).addClass("slick-initialized"),t.buildRows(),t.buildOut(),t.setProps(),t.startLoad(),t.loadSlider(),t.initializeEvents(),t.updateArrows(),t.updateDots(),t.checkResponsive(!0),t.focusHandler()),e&&t.$slider.trigger("init",[t]),!0===t.options.accessibility&&t.initADA(),t.options.autoplay&&(t.paused=!1,t.autoPlay())},e.prototype.initADA=function(){var e=this,t=Math.ceil(e.slideCount/e.options.slidesToShow),o=e.getNavigableIndexes().filter(function(i){return i>=0&&i<e.slideCount});e.$slides.add(e.$slideTrack.find(".slick-cloned")).attr({"aria-hidden":"true",tabindex:"-1"}).find("a, input, button, select").attr({tabindex:"-1"}),null!==e.$dots&&(e.$slides.not(e.$slideTrack.find(".slick-cloned")).each(function(t){var s=o.indexOf(t);i(this).attr({role:"tabpanel",id:"slick-slide"+e.instanceUid+t,tabindex:-1}),-1!==s&&i(this).attr({"aria-describedby":"slick-slide-control"+e.instanceUid+s})}),e.$dots.attr("role","tablist").find("li").each(function(s){var n=o[s];i(this).attr({role:"presentation"}),i(this).find("button").first().attr({role:"tab",id:"slick-slide-control"+e.instanceUid+s,"aria-controls":"slick-slide"+e.instanceUid+n,"aria-label":s+1+" of "+t,"aria-selected":null,tabindex:"-1"})}).eq(e.currentSlide).find("button").attr({"aria-selected":"true",tabindex:"0"}).end());for(var s=e.currentSlide,n=s+e.options.slidesToShow;s<n;s++)e.$slides.eq(s).attr("tabindex",0);e.activateADA()},e.prototype.initArrowEvents=function(){var i=this;!0===i.options.arrows&&i.slideCount>i.options.slidesToShow&&(i.$prevArrow.off("click.slick").on("click.slick",{message:"previous"},i.changeSlide),i.$nextArrow.off("click.slick").on("click.slick",{message:"next"},i.changeSlide),!0===i.options.accessibility&&(i.$prevArrow.on("keydown.slick",i.keyHandler),i.$nextArrow.on("keydown.slick",i.keyHandler)))},e.prototype.initDotEvents=function(){var e=this;!0===e.options.dots&&(i("li",e.$dots).on("click.slick",{message:"index"},e.changeSlide),!0===e.options.accessibility&&e.$dots.on("keydown.slick",e.keyHandler)),!0===e.options.dots&&!0===e.options.pauseOnDotsHover&&i("li",e.$dots).on("mouseenter.slick",i.proxy(e.interrupt,e,!0)).on("mouseleave.slick",i.proxy(e.interrupt,e,!1))},e.prototype.initSlideEvents=function(){var e=this;e.options.pauseOnHover&&(e.$list.on("mouseenter.slick",i.proxy(e.interrupt,e,!0)),e.$list.on("mouseleave.slick",i.proxy(e.interrupt,e,!1)))},e.prototype.initializeEvents=function(){var e=this;e.initArrowEvents(),e.initDotEvents(),e.initSlideEvents(),e.$list.on("touchstart.slick mousedown.slick",{action:"start"},e.swipeHandler),e.$list.on("touchmove.slick mousemove.slick",{action:"move"},e.swipeHandler),e.$list.on("touchend.slick mouseup.slick",{action:"end"},e.swipeHandler),e.$list.on("touchcancel.slick mouseleave.slick",{action:"end"},e.swipeHandler),e.$list.on("click.slick",e.clickHandler),i(document).on(e.visibilityChange,i.proxy(e.visibility,e)),!0===e.options.accessibility&&e.$list.on("keydown.slick",e.keyHandler),!0===e.options.focusOnSelect&&i(e.$slideTrack).children().on("click.slick",e.selectHandler),i(window).on("orientationchange.slick.slick-"+e.instanceUid,i.proxy(e.orientationChange,e)),i(window).on("resize.slick.slick-"+e.instanceUid,i.proxy(e.resize,e)),i("[draggable!=true]",e.$slideTrack).on("dragstart",e.preventDefault),i(window).on("load.slick.slick-"+e.instanceUid,e.setPosition),i(e.setPosition)},e.prototype.initUI=function(){var i=this;!0===i.options.arrows&&i.slideCount>i.options.slidesToShow&&(i.$prevArrow.show(),i.$nextArrow.show()),!0===i.options.dots&&i.slideCount>i.options.slidesToShow&&i.$dots.show()},e.prototype.keyHandler=function(i){var e=this;i.target.tagName.match("TEXTAREA|INPUT|SELECT")||(37===i.keyCode&&!0===e.options.accessibility?e.changeSlide({data:{message:!0===e.options.rtl?"next":"previous"}}):39===i.keyCode&&!0===e.options.accessibility&&e.changeSlide({data:{message:!0===e.options.rtl?"previous":"next"}}))},e.prototype.lazyLoad=function(){function e(e){i("img[data-lazy]",e).each(function(){var e=i(this),t=i(this).attr("data-lazy"),o=i(this).attr("data-srcset"),s=i(this).attr("data-sizes")||n.$slider.attr("data-sizes"),r=document.createElement("img");r.onload=function(){e.animate({opacity:0},100,function(){o&&(e.attr("srcset",o),s&&e.attr("sizes",s)),e.attr("src",t).animate({opacity:1},200,function(){e.removeAttr("data-lazy data-srcset data-sizes").removeClass("slick-loading")}),n.$slider.trigger("lazyLoaded",[n,e,t])})},r.onerror=function(){e.removeAttr("data-lazy").removeClass("slick-loading").addClass("slick-lazyload-error"),n.$slider.trigger("lazyLoadError",[n,e,t])},r.src=t})}var t,o,s,n=this;if(!0===n.options.centerMode?!0===n.options.infinite?s=(o=n.currentSlide+(n.options.slidesToShow/2+1))+n.options.slidesToShow+2:(o=Math.max(0,n.currentSlide-(n.options.slidesToShow/2+1)),s=n.options.slidesToShow/2+1+2+n.currentSlide):(o=n.options.infinite?n.options.slidesToShow+n.currentSlide:n.currentSlide,s=Math.ceil(o+n.options.slidesToShow),!0===n.options.fade&&(o>0&&o--,s<=n.slideCount&&s++)),t=n.$slider.find(".slick-slide").slice(o,s),"anticipated"===n.options.lazyLoad)for(var r=o-1,l=s,d=n.$slider.find(".slick-slide"),a=0;a<n.options.slidesToScroll;a++)r<0&&(r=n.slideCount-1),t=(t=t.add(d.eq(r))).add(d.eq(l)),r--,l++;e(t),n.slideCount<=n.options.slidesToShow?e(n.$slider.find(".slick-slide")):n.currentSlide>=n.slideCount-n.options.slidesToShow?e(n.$slider.find(".slick-cloned").slice(0,n.options.slidesToShow)):0===n.currentSlide&&e(n.$slider.find(".slick-cloned").slice(-1*n.options.slidesToShow))},e.prototype.loadSlider=function(){var i=this;i.setPosition(),i.$slideTrack.css({opacity:1}),i.$slider.removeClass("slick-loading"),i.initUI(),"progressive"===i.options.lazyLoad&&i.progressiveLazyLoad()},e.prototype.next=e.prototype.slickNext=function(){this.changeSlide({data:{message:"next"}})},e.prototype.orientationChange=function(){var i=this;i.checkResponsive(),i.setPosition()},e.prototype.pause=e.prototype.slickPause=function(){var i=this;i.autoPlayClear(),i.paused=!0},e.prototype.play=e.prototype.slickPlay=function(){var i=this;i.autoPlay(),i.options.autoplay=!0,i.paused=!1,i.focussed=!1,i.interrupted=!1},e.prototype.postSlide=function(e){var t=this;t.unslicked||(t.$slider.trigger("afterChange",[t,e]),t.animating=!1,t.slideCount>t.options.slidesToShow&&t.setPosition(),t.swipeLeft=null,t.options.autoplay&&t.autoPlay(),!0===t.options.accessibility&&(t.initADA(),t.options.focusOnChange&&i(t.$slides.get(t.currentSlide)).attr("tabindex",0).focus()))},e.prototype.prev=e.prototype.slickPrev=function(){this.changeSlide({data:{message:"previous"}})},e.prototype.preventDefault=function(i){i.preventDefault()},e.prototype.progressiveLazyLoad=function(e){e=e||1;var t,o,s,n,r,l=this,d=i("img[data-lazy]",l.$slider);d.length?(t=d.first(),o=t.attr("data-lazy"),s=t.attr("data-srcset"),n=t.attr("data-sizes")||l.$slider.attr("data-sizes"),(r=document.createElement("img")).onload=function(){s&&(t.attr("srcset",s),n&&t.attr("sizes",n)),t.attr("src",o).removeAttr("data-lazy data-srcset data-sizes").removeClass("slick-loading"),!0===l.options.adaptiveHeight&&l.setPosition(),l.$slider.trigger("lazyLoaded",[l,t,o]),l.progressiveLazyLoad()},r.onerror=function(){e<3?setTimeout(function(){l.progressiveLazyLoad(e+1)},500):(t.removeAttr("data-lazy").removeClass("slick-loading").addClass("slick-lazyload-error"),l.$slider.trigger("lazyLoadError",[l,t,o]),l.progressiveLazyLoad())},r.src=o):l.$slider.trigger("allImagesLoaded",[l])},e.prototype.refresh=function(e){var t,o,s=this;o=s.slideCount-s.options.slidesToShow,!s.options.infinite&&s.currentSlide>o&&(s.currentSlide=o),s.slideCount<=s.options.slidesToShow&&(s.currentSlide=0),t=s.currentSlide,s.destroy(!0),i.extend(s,s.initials,{currentSlide:t}),s.init(),e||s.changeSlide({data:{message:"index",index:t}},!1)},e.prototype.registerBreakpoints=function(){var e,t,o,s=this,n=s.options.responsive||null;if("array"===i.type(n)&&n.length){s.respondTo=s.options.respondTo||"window";for(e in n)if(o=s.breakpoints.length-1,n.hasOwnProperty(e)){for(t=n[e].breakpoint;o>=0;)s.breakpoints[o]&&s.breakpoints[o]===t&&s.breakpoints.splice(o,1),o--;s.breakpoints.push(t),s.breakpointSettings[t]=n[e].settings}s.breakpoints.sort(function(i,e){return s.options.mobileFirst?i-e:e-i})}},e.prototype.reinit=function(){var e=this;e.$slides=e.$slideTrack.children(e.options.slide).addClass("slick-slide"),e.slideCount=e.$slides.length,e.currentSlide>=e.slideCount&&0!==e.currentSlide&&(e.currentSlide=e.currentSlide-e.options.slidesToScroll),e.slideCount<=e.options.slidesToShow&&(e.currentSlide=0),e.registerBreakpoints(),e.setProps(),e.setupInfinite(),e.buildArrows(),e.updateArrows(),e.initArrowEvents(),e.buildDots(),e.updateDots(),e.initDotEvents(),e.cleanUpSlideEvents(),e.initSlideEvents(),e.checkResponsive(!1,!0),!0===e.options.focusOnSelect&&i(e.$slideTrack).children().on("click.slick",e.selectHandler),e.setSlideClasses("number"==typeof e.currentSlide?e.currentSlide:0),e.setPosition(),e.focusHandler(),e.paused=!e.options.autoplay,e.autoPlay(),e.$slider.trigger("reInit",[e])},e.prototype.resize=function(){var e=this;i(window).width()!==e.windowWidth&&(clearTimeout(e.windowDelay),e.windowDelay=window.setTimeout(function(){e.windowWidth=i(window).width(),e.checkResponsive(),e.unslicked||e.setPosition()},50))},e.prototype.removeSlide=e.prototype.slickRemove=function(i,e,t){var o=this;if(i="boolean"==typeof i?!0===(e=i)?0:o.slideCount-1:!0===e?--i:i,o.slideCount<1||i<0||i>o.slideCount-1)return!1;o.unload(),!0===t?o.$slideTrack.children().remove():o.$slideTrack.children(this.options.slide).eq(i).remove(),o.$slides=o.$slideTrack.children(this.options.slide),o.$slideTrack.children(this.options.slide).detach(),o.$slideTrack.append(o.$slides),o.$slidesCache=o.$slides,o.reinit()},e.prototype.setCSS=function(i){var e,t,o=this,s={};!0===o.options.rtl&&(i=-i),e="left"==o.positionProp?Math.ceil(i)+"px":"0px",t="top"==o.positionProp?Math.ceil(i)+"px":"0px",s[o.positionProp]=i,!1===o.transformsEnabled?o.$slideTrack.css(s):(s={},!1===o.cssTransitions?(s[o.animType]="translate("+e+", "+t+")",o.$slideTrack.css(s)):(s[o.animType]="translate3d("+e+", "+t+", 0px)",o.$slideTrack.css(s)))},e.prototype.setDimensions=function(){var i=this;!1===i.options.vertical?!0===i.options.centerMode&&i.$list.css({padding:"0px "+i.options.centerPadding}):(i.$list.height(i.$slides.first().outerHeight(!0)*i.options.slidesToShow),!0===i.options.centerMode&&i.$list.css({padding:i.options.centerPadding+" 0px"})),i.listWidth=i.$list.width(),i.listHeight=i.$list.height(),!1===i.options.vertical&&!1===i.options.variableWidth?(i.slideWidth=Math.ceil(i.listWidth/i.options.slidesToShow),i.$slideTrack.width(Math.ceil(i.slideWidth*i.$slideTrack.children(".slick-slide").length))):!0===i.options.variableWidth?i.$slideTrack.width(5e3*i.slideCount):(i.slideWidth=Math.ceil(i.listWidth),i.$slideTrack.height(Math.ceil(i.$slides.first().outerHeight(!0)*i.$slideTrack.children(".slick-slide").length)));var e=i.$slides.first().outerWidth(!0)-i.$slides.first().width();!1===i.options.variableWidth&&i.$slideTrack.children(".slick-slide").width(i.slideWidth-e)},e.prototype.setFade=function(){var e,t=this;t.$slides.each(function(o,s){e=t.slideWidth*o*-1,!0===t.options.rtl?i(s).css({position:"relative",right:e,top:0,zIndex:t.options.zIndex-2,opacity:0}):i(s).css({position:"relative",left:e,top:0,zIndex:t.options.zIndex-2,opacity:0})}),t.$slides.eq(t.currentSlide).css({zIndex:t.options.zIndex-1,opacity:1})},e.prototype.setHeight=function(){var i=this;if(1===i.options.slidesToShow&&!0===i.options.adaptiveHeight&&!1===i.options.vertical){var e=i.$slides.eq(i.currentSlide).outerHeight(!0);i.$list.css("height",e)}},e.prototype.setOption=e.prototype.slickSetOption=function(){var e,t,o,s,n,r=this,l=!1;if("object"===i.type(arguments[0])?(o=arguments[0],l=arguments[1],n="multiple"):"string"===i.type(arguments[0])&&(o=arguments[0],s=arguments[1],l=arguments[2],"responsive"===arguments[0]&&"array"===i.type(arguments[1])?n="responsive":void 0!==arguments[1]&&(n="single")),"single"===n)r.options[o]=s;else if("multiple"===n)i.each(o,function(i,e){r.options[i]=e});else if("responsive"===n)for(t in s)if("array"!==i.type(r.options.responsive))r.options.responsive=[s[t]];else{for(e=r.options.responsive.length-1;e>=0;)r.options.responsive[e].breakpoint===s[t].breakpoint&&r.options.responsive.splice(e,1),e--;r.options.responsive.push(s[t])}l&&(r.unload(),r.reinit())},e.prototype.setPosition=function(){var i=this;i.setDimensions(),i.setHeight(),!1===i.options.fade?i.setCSS(i.getLeft(i.currentSlide)):i.setFade(),i.$slider.trigger("setPosition",[i])},e.prototype.setProps=function(){var i=this,e=document.body.style;i.positionProp=!0===i.options.vertical?"top":"left","top"===i.positionProp?i.$slider.addClass("slick-vertical"):i.$slider.removeClass("slick-vertical"),void 0===e.WebkitTransition&&void 0===e.MozTransition&&void 0===e.msTransition||!0===i.options.useCSS&&(i.cssTransitions=!0),i.options.fade&&("number"==typeof i.options.zIndex?i.options.zIndex<3&&(i.options.zIndex=3):i.options.zIndex=i.defaults.zIndex),void 0!==e.OTransform&&(i.animType="OTransform",i.transformType="-o-transform",i.transitionType="OTransition",void 0===e.perspectiveProperty&&void 0===e.webkitPerspective&&(i.animType=!1)),void 0!==e.MozTransform&&(i.animType="MozTransform",i.transformType="-moz-transform",i.transitionType="MozTransition",void 0===e.perspectiveProperty&&void 0===e.MozPerspective&&(i.animType=!1)),void 0!==e.webkitTransform&&(i.animType="webkitTransform",i.transformType="-webkit-transform",i.transitionType="webkitTransition",void 0===e.perspectiveProperty&&void 0===e.webkitPerspective&&(i.animType=!1)),void 0!==e.msTransform&&(i.animType="msTransform",i.transformType="-ms-transform",i.transitionType="msTransition",void 0===e.msTransform&&(i.animType=!1)),void 0!==e.transform&&!1!==i.animType&&(i.animType="transform",i.transformType="transform",i.transitionType="transition"),i.transformsEnabled=i.options.useTransform&&null!==i.animType&&!1!==i.animType},e.prototype.setSlideClasses=function(i){var e,t,o,s,n=this;if(t=n.$slider.find(".slick-slide").removeClass("slick-active slick-center slick-current").attr("aria-hidden","true"),n.$slides.eq(i).addClass("slick-current"),!0===n.options.centerMode){var r=n.options.slidesToShow%2==0?1:0;e=Math.floor(n.options.slidesToShow/2),!0===n.options.infinite&&(i>=e&&i<=n.slideCount-1-e?n.$slides.slice(i-e+r,i+e+1).addClass("slick-active").attr("aria-hidden","false"):(o=n.options.slidesToShow+i,t.slice(o-e+1+r,o+e+2).addClass("slick-active").attr("aria-hidden","false")),0===i?t.eq(t.length-1-n.options.slidesToShow).addClass("slick-center"):i===n.slideCount-1&&t.eq(n.options.slidesToShow).addClass("slick-center")),n.$slides.eq(i).addClass("slick-center")}else i>=0&&i<=n.slideCount-n.options.slidesToShow?n.$slides.slice(i,i+n.options.slidesToShow).addClass("slick-active").attr("aria-hidden","false"):t.length<=n.options.slidesToShow?t.addClass("slick-active").attr("aria-hidden","false"):(s=n.slideCount%n.options.slidesToShow,o=!0===n.options.infinite?n.options.slidesToShow+i:i,n.options.slidesToShow==n.options.slidesToScroll&&n.slideCount-i<n.options.slidesToShow?t.slice(o-(n.options.slidesToShow-s),o+s).addClass("slick-active").attr("aria-hidden","false"):t.slice(o,o+n.options.slidesToShow).addClass("slick-active").attr("aria-hidden","false"));"ondemand"!==n.options.lazyLoad&&"anticipated"!==n.options.lazyLoad||n.lazyLoad()},e.prototype.setupInfinite=function(){var e,t,o,s=this;if(!0===s.options.fade&&(s.options.centerMode=!1),!0===s.options.infinite&&!1===s.options.fade&&(t=null,s.slideCount>s.options.slidesToShow)){for(o=!0===s.options.centerMode?s.options.slidesToShow+1:s.options.slidesToShow,e=s.slideCount;e>s.slideCount-o;e-=1)t=e-1,i(s.$slides[t]).clone(!0).attr("id","").attr("data-slick-index",t-s.slideCount).prependTo(s.$slideTrack).addClass("slick-cloned");for(e=0;e<o+s.slideCount;e+=1)t=e,i(s.$slides[t]).clone(!0).attr("id","").attr("data-slick-index",t+s.slideCount).appendTo(s.$slideTrack).addClass("slick-cloned");s.$slideTrack.find(".slick-cloned").find("[id]").each(function(){i(this).attr("id","")})}},e.prototype.interrupt=function(i){var e=this;i||e.autoPlay(),e.interrupted=i},e.prototype.selectHandler=function(e){var t=this,o=i(e.target).is(".slick-slide")?i(e.target):i(e.target).parents(".slick-slide"),s=parseInt(o.attr("data-slick-index"));s||(s=0),t.slideCount<=t.options.slidesToShow?t.slideHandler(s,!1,!0):t.slideHandler(s)},e.prototype.slideHandler=function(i,e,t){var o,s,n,r,l,d=null,a=this;if(e=e||!1,!(!0===a.animating&&!0===a.options.waitForAnimate||!0===a.options.fade&&a.currentSlide===i))if(!1===e&&a.asNavFor(i),o=i,d=a.getLeft(o),r=a.getLeft(a.currentSlide),a.currentLeft=null===a.swipeLeft?r:a.swipeLeft,!1===a.options.infinite&&!1===a.options.centerMode&&(i<0||i>a.getDotCount()*a.options.slidesToScroll))!1===a.options.fade&&(o=a.currentSlide,!0!==t?a.animateSlide(r,function(){a.postSlide(o)}):a.postSlide(o));else if(!1===a.options.infinite&&!0===a.options.centerMode&&(i<0||i>a.slideCount-a.options.slidesToScroll))!1===a.options.fade&&(o=a.currentSlide,!0!==t?a.animateSlide(r,function(){a.postSlide(o)}):a.postSlide(o));else{if(a.options.autoplay&&clearInterval(a.autoPlayTimer),s=o<0?a.slideCount%a.options.slidesToScroll!=0?a.slideCount-a.slideCount%a.options.slidesToScroll:a.slideCount+o:o>=a.slideCount?a.slideCount%a.options.slidesToScroll!=0?0:o-a.slideCount:o,a.animating=!0,a.$slider.trigger("beforeChange",[a,a.currentSlide,s]),n=a.currentSlide,a.currentSlide=s,a.setSlideClasses(a.currentSlide),a.options.asNavFor&&(l=(l=a.getNavTarget()).slick("getSlick")).slideCount<=l.options.slidesToShow&&l.setSlideClasses(a.currentSlide),a.updateDots(),a.updateArrows(),!0===a.options.fade)return!0!==t?(a.fadeSlideOut(n),a.fadeSlide(s,function(){a.postSlide(s)})):a.postSlide(s),void a.animateHeight();!0!==t?a.animateSlide(d,function(){a.postSlide(s)}):a.postSlide(s)}},e.prototype.startLoad=function(){var i=this;!0===i.options.arrows&&i.slideCount>i.options.slidesToShow&&(i.$prevArrow.hide(),i.$nextArrow.hide()),!0===i.options.dots&&i.slideCount>i.options.slidesToShow&&i.$dots.hide(),i.$slider.addClass("slick-loading")},e.prototype.swipeDirection=function(){var i,e,t,o,s=this;return i=s.touchObject.startX-s.touchObject.curX,e=s.touchObject.startY-s.touchObject.curY,t=Math.atan2(e,i),(o=Math.round(180*t/Math.PI))<0&&(o=360-Math.abs(o)),o<=45&&o>=0?!1===s.options.rtl?"left":"right":o<=360&&o>=315?!1===s.options.rtl?"left":"right":o>=135&&o<=225?!1===s.options.rtl?"right":"left":!0===s.options.verticalSwiping?o>=35&&o<=135?"down":"up":"vertical"},e.prototype.swipeEnd=function(i){var e,t,o=this;if(o.dragging=!1,o.swiping=!1,o.scrolling)return o.scrolling=!1,!1;if(o.interrupted=!1,o.shouldClick=!(o.touchObject.swipeLength>10),void 0===o.touchObject.curX)return!1;if(!0===o.touchObject.edgeHit&&o.$slider.trigger("edge",[o,o.swipeDirection()]),o.touchObject.swipeLength>=o.touchObject.minSwipe){switch(t=o.swipeDirection()){case"left":case"down":e=o.options.swipeToSlide?o.checkNavigable(o.currentSlide+o.getSlideCount()):o.currentSlide+o.getSlideCount(),o.currentDirection=0;break;case"right":case"up":e=o.options.swipeToSlide?o.checkNavigable(o.currentSlide-o.getSlideCount()):o.currentSlide-o.getSlideCount(),o.currentDirection=1}"vertical"!=t&&(o.slideHandler(e),o.touchObject={},o.$slider.trigger("swipe",[o,t]))}else o.touchObject.startX!==o.touchObject.curX&&(o.slideHandler(o.currentSlide),o.touchObject={})},e.prototype.swipeHandler=function(i){var e=this;if(!(!1===e.options.swipe||"ontouchend"in document&&!1===e.options.swipe||!1===e.options.draggable&&-1!==i.type.indexOf("mouse")))switch(e.touchObject.fingerCount=i.originalEvent&&void 0!==i.originalEvent.touches?i.originalEvent.touches.length:1,e.touchObject.minSwipe=e.listWidth/e.options.touchThreshold,!0===e.options.verticalSwiping&&(e.touchObject.minSwipe=e.listHeight/e.options.touchThreshold),i.data.action){case"start":e.swipeStart(i);break;case"move":e.swipeMove(i);break;case"end":e.swipeEnd(i)}},e.prototype.swipeMove=function(i){var e,t,o,s,n,r,l=this;return n=void 0!==i.originalEvent?i.originalEvent.touches:null,!(!l.dragging||l.scrolling||n&&1!==n.length)&&(e=l.getLeft(l.currentSlide),l.touchObject.curX=void 0!==n?n[0].pageX:i.clientX,l.touchObject.curY=void 0!==n?n[0].pageY:i.clientY,l.touchObject.swipeLength=Math.round(Math.sqrt(Math.pow(l.touchObject.curX-l.touchObject.startX,2))),r=Math.round(Math.sqrt(Math.pow(l.touchObject.curY-l.touchObject.startY,2))),!l.options.verticalSwiping&&!l.swiping&&r>4?(l.scrolling=!0,!1):(!0===l.options.verticalSwiping&&(l.touchObject.swipeLength=r),t=l.swipeDirection(),void 0!==i.originalEvent&&l.touchObject.swipeLength>4&&(l.swiping=!0,i.preventDefault()),s=(!1===l.options.rtl?1:-1)*(l.touchObject.curX>l.touchObject.startX?1:-1),!0===l.options.verticalSwiping&&(s=l.touchObject.curY>l.touchObject.startY?1:-1),o=l.touchObject.swipeLength,l.touchObject.edgeHit=!1,!1===l.options.infinite&&(0===l.currentSlide&&"right"===t||l.currentSlide>=l.getDotCount()&&"left"===t)&&(o=l.touchObject.swipeLength*l.options.edgeFriction,l.touchObject.edgeHit=!0),!1===l.options.vertical?l.swipeLeft=e+o*s:l.swipeLeft=e+o*(l.$list.height()/l.listWidth)*s,!0===l.options.verticalSwiping&&(l.swipeLeft=e+o*s),!0!==l.options.fade&&!1!==l.options.touchMove&&(!0===l.animating?(l.swipeLeft=null,!1):void l.setCSS(l.swipeLeft))))},e.prototype.swipeStart=function(i){var e,t=this;if(t.interrupted=!0,1!==t.touchObject.fingerCount||t.slideCount<=t.options.slidesToShow)return t.touchObject={},!1;void 0!==i.originalEvent&&void 0!==i.originalEvent.touches&&(e=i.originalEvent.touches[0]),t.touchObject.startX=t.touchObject.curX=void 0!==e?e.pageX:i.clientX,t.touchObject.startY=t.touchObject.curY=void 0!==e?e.pageY:i.clientY,t.dragging=!0},e.prototype.unfilterSlides=e.prototype.slickUnfilter=function(){var i=this;null!==i.$slidesCache&&(i.unload(),i.$slideTrack.children(this.options.slide).detach(),i.$slidesCache.appendTo(i.$slideTrack),i.reinit())},e.prototype.unload=function(){var e=this;i(".slick-cloned",e.$slider).remove(),e.$dots&&e.$dots.remove(),e.$prevArrow&&e.htmlExpr.test(e.options.prevArrow)&&e.$prevArrow.remove(),e.$nextArrow&&e.htmlExpr.test(e.options.nextArrow)&&e.$nextArrow.remove(),e.$slides.removeClass("slick-slide slick-active slick-visible slick-current").attr("aria-hidden","true").css("width","")},e.prototype.unslick=function(i){var e=this;e.$slider.trigger("unslick",[e,i]),e.destroy()},e.prototype.updateArrows=function(){var i=this;Math.floor(i.options.slidesToShow/2),!0===i.options.arrows&&i.slideCount>i.options.slidesToShow&&!i.options.infinite&&(i.$prevArrow.removeClass("slick-disabled").attr("aria-disabled","false"),i.$nextArrow.removeClass("slick-disabled").attr("aria-disabled","false"),0===i.currentSlide?(i.$prevArrow.addClass("slick-disabled").attr("aria-disabled","true"),i.$nextArrow.removeClass("slick-disabled").attr("aria-disabled","false")):i.currentSlide>=i.slideCount-i.options.slidesToShow&&!1===i.options.centerMode?(i.$nextArrow.addClass("slick-disabled").attr("aria-disabled","true"),i.$prevArrow.removeClass("slick-disabled").attr("aria-disabled","false")):i.currentSlide>=i.slideCount-1&&!0===i.options.centerMode&&(i.$nextArrow.addClass("slick-disabled").attr("aria-disabled","true"),i.$prevArrow.removeClass("slick-disabled").attr("aria-disabled","false")))},e.prototype.updateDots=function(){var i=this;null!==i.$dots&&(i.$dots.find("li").removeClass("slick-active").end(),i.$dots.find("li").eq(Math.floor(i.currentSlide/i.options.slidesToScroll)).addClass("slick-active"))},e.prototype.visibility=function(){var i=this;i.options.autoplay&&(document[i.hidden]?i.interrupted=!0:i.interrupted=!1)},i.fn.slick=function(){var i,t,o=this,s=arguments[0],n=Array.prototype.slice.call(arguments,1),r=o.length;for(i=0;i<r;i++)if("object"==typeof s||void 0===s?o[i].slick=new e(o[i],s):t=o[i].slick[s].apply(o[i].slick,n),void 0!==t)return t;return o}});


/*!
 * The Final Countdown for jQuery v2.1.0 (http://hilios.github.io/jQuery.countdown/)
 * Copyright (c) 2015 Edson Hilios
 * 
 * Permission is hereby granted, free of charge, to any person obtaining a copy of
 * this software and associated documentation files (the "Software"), to deal in
 * the Software without restriction, including without limitation the rights to
 * use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
 * the Software, and to permit persons to whom the Software is furnished to do so,
 * subject to the following conditions:
 * 
 * The above copyright notice and this permission notice shall be included in all
 * copies or substantial portions of the Software.
 * 
 * THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 * IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
 * FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
 * COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
 * IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
 * CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
 */
!function(a){"use strict";"function"==typeof define&&define.amd?define(["jquery"],a):a(jQuery)}(function(a){"use strict";function b(a){if(a instanceof Date)return a;if(String(a).match(g))return String(a).match(/^[0-9]*$/)&&(a=Number(a)),String(a).match(/\-/)&&(a=String(a).replace(/\-/g,"/")),new Date(a);throw new Error("Couldn't cast `"+a+"` to a date object.")}function c(a){var b=a.toString().replace(/([.?*+^$[\]\\(){}|-])/g,"\\$1");return new RegExp(b)}function d(a){return function(b){var d=b.match(/%(-|!)?[A-Z]{1}(:[^;]+;)?/gi);if(d)for(var f=0,g=d.length;g>f;++f){var h=d[f].match(/%(-|!)?([a-zA-Z]{1})(:[^;]+;)?/),j=c(h[0]),k=h[1]||"",l=h[3]||"",m=null;h=h[2],i.hasOwnProperty(h)&&(m=i[h],m=Number(a[m])),null!==m&&("!"===k&&(m=e(l,m)),""===k&&10>m&&(m="0"+m.toString()),b=b.replace(j,m.toString()))}return b=b.replace(/%%/,"%")}}function e(a,b){var c="s",d="";return a&&(a=a.replace(/(:|;|\s)/gi,"").split(/\,/),1===a.length?c=a[0]:(d=a[0],c=a[1])),1===Math.abs(b)?d:c}var f=[],g=[],h={precision:100,elapse:!1};g.push(/^[0-9]*$/.source),g.push(/([0-9]{1,2}\/){2}[0-9]{4}( [0-9]{1,2}(:[0-9]{2}){2})?/.source),g.push(/[0-9]{4}([\/\-][0-9]{1,2}){2}( [0-9]{1,2}(:[0-9]{2}){2})?/.source),g=new RegExp(g.join("|"));var i={Y:"years",m:"months",n:"daysToMonth",w:"weeks",d:"daysToWeek",D:"totalDays",H:"hours",M:"minutes",S:"seconds"},j=function(b,c,d){this.el=b,this.$el=a(b),this.interval=null,this.offset={},this.options=a.extend({},h),this.instanceNumber=f.length,f.push(this),this.$el.data("countdown-instance",this.instanceNumber),d&&("function"==typeof d?(this.$el.on("update.countdown",d),this.$el.on("stoped.countdown",d),this.$el.on("finish.countdown",d)):this.options=a.extend({},h,d)),this.setFinalDate(c),this.start()};a.extend(j.prototype,{start:function(){null!==this.interval&&clearInterval(this.interval);var a=this;this.update(),this.interval=setInterval(function(){a.update.call(a)},this.options.precision)},stop:function(){clearInterval(this.interval),this.interval=null,this.dispatchEvent("stoped")},toggle:function(){this.interval?this.stop():this.start()},pause:function(){this.stop()},resume:function(){this.start()},remove:function(){this.stop.call(this),f[this.instanceNumber]=null,delete this.$el.data().countdownInstance},setFinalDate:function(a){this.finalDate=b(a)},update:function(){if(0===this.$el.closest("html").length)return void this.remove();var b,c=void 0!==a._data(this.el,"events"),d=new Date;b=this.finalDate.getTime()-d.getTime(),b=Math.ceil(b/1e3),b=!this.options.elapse&&0>b?0:Math.abs(b),this.totalSecsLeft!==b&&c&&(this.totalSecsLeft=b,this.elapsed=d>=this.finalDate,this.offset={seconds:this.totalSecsLeft%60,minutes:Math.floor(this.totalSecsLeft/60)%60,hours:Math.floor(this.totalSecsLeft/60/60)%24,days:Math.floor(this.totalSecsLeft/60/60/24)%7,daysToWeek:Math.floor(this.totalSecsLeft/60/60/24)%7,daysToMonth:Math.floor(this.totalSecsLeft/60/60/24%30.4368),totalDays:Math.floor(this.totalSecsLeft/60/60/24),weeks:Math.floor(this.totalSecsLeft/60/60/24/7),months:Math.floor(this.totalSecsLeft/60/60/24/30.4368),years:Math.abs(this.finalDate.getFullYear()-d.getFullYear())},this.options.elapse||0!==this.totalSecsLeft?this.dispatchEvent("update"):(this.stop(),this.dispatchEvent("finish")))},dispatchEvent:function(b){var c=a.Event(b+".countdown");c.finalDate=this.finalDate,c.elapsed=this.elapsed,c.offset=a.extend({},this.offset),c.strftime=d(this.offset),this.$el.trigger(c)}}),a.fn.countdown=function(){var b=Array.prototype.slice.call(arguments,0);return this.each(function(){var c=a(this).data("countdown-instance");if(void 0!==c){var d=f[c],e=b[0];j.prototype.hasOwnProperty(e)?d[e].apply(d,b.slice(1)):null===String(e).match(/^[$A-Z_][0-9A-Z_$]*$/i)?(d.setFinalDate.call(d,e),d.start()):a.error("Method %s does not exist on jQuery.countdown".replace(/\%s/gi,e))}else new j(this,b[0],b[1])})}});



/*
 * google code-prettify
 */
!function(){var q=null;window.PR_SHOULD_USE_CONTINUATION=!0;
    (function(){function S(a){function d(e){var b=e.charCodeAt(0);if(b!==92)return b;var a=e.charAt(1);return(b=r[a])?b:"0"<=a&&a<="7"?parseInt(e.substring(1),8):a==="u"||a==="x"?parseInt(e.substring(2),16):e.charCodeAt(1)}function g(e){if(e<32)return(e<16?"\\x0":"\\x")+e.toString(16);e=String.fromCharCode(e);return e==="\\"||e==="-"||e==="]"||e==="^"?"\\"+e:e}function b(e){var b=e.substring(1,e.length-1).match(/\\u[\dA-Fa-f]{4}|\\x[\dA-Fa-f]{2}|\\[0-3][0-7]{0,2}|\\[0-7]{1,2}|\\[\S\s]|[^\\]/g),e=[],a=
    b[0]==="^",c=["["];a&&c.push("^");for(var a=a?1:0,f=b.length;a<f;++a){var h=b[a];if(/\\[bdsw]/i.test(h))c.push(h);else{var h=d(h),l;a+2<f&&"-"===b[a+1]?(l=d(b[a+2]),a+=2):l=h;e.push([h,l]);l<65||h>122||(l<65||h>90||e.push([Math.max(65,h)|32,Math.min(l,90)|32]),l<97||h>122||e.push([Math.max(97,h)&-33,Math.min(l,122)&-33]))}}e.sort(function(e,a){return e[0]-a[0]||a[1]-e[1]});b=[];f=[];for(a=0;a<e.length;++a)h=e[a],h[0]<=f[1]+1?f[1]=Math.max(f[1],h[1]):b.push(f=h);for(a=0;a<b.length;++a)h=b[a],c.push(g(h[0])),
    h[1]>h[0]&&(h[1]+1>h[0]&&c.push("-"),c.push(g(h[1])));c.push("]");return c.join("")}function s(e){for(var a=e.source.match(/\[(?:[^\\\]]|\\[\S\s])*]|\\u[\dA-Fa-f]{4}|\\x[\dA-Fa-f]{2}|\\\d+|\\[^\dux]|\(\?[!:=]|[()^]|[^()[\\^]+/g),c=a.length,d=[],f=0,h=0;f<c;++f){var l=a[f];l==="("?++h:"\\"===l.charAt(0)&&(l=+l.substring(1))&&(l<=h?d[l]=-1:a[f]=g(l))}for(f=1;f<d.length;++f)-1===d[f]&&(d[f]=++x);for(h=f=0;f<c;++f)l=a[f],l==="("?(++h,d[h]||(a[f]="(?:")):"\\"===l.charAt(0)&&(l=+l.substring(1))&&l<=h&&
    (a[f]="\\"+d[l]);for(f=0;f<c;++f)"^"===a[f]&&"^"!==a[f+1]&&(a[f]="");if(e.ignoreCase&&m)for(f=0;f<c;++f)l=a[f],e=l.charAt(0),l.length>=2&&e==="["?a[f]=b(l):e!=="\\"&&(a[f]=l.replace(/[A-Za-z]/g,function(a){a=a.charCodeAt(0);return"["+String.fromCharCode(a&-33,a|32)+"]"}));return a.join("")}for(var x=0,m=!1,j=!1,k=0,c=a.length;k<c;++k){var i=a[k];if(i.ignoreCase)j=!0;else if(/[a-z]/i.test(i.source.replace(/\\u[\da-f]{4}|\\x[\da-f]{2}|\\[^UXux]/gi,""))){m=!0;j=!1;break}}for(var r={b:8,t:9,n:10,v:11,
    f:12,r:13},n=[],k=0,c=a.length;k<c;++k){i=a[k];if(i.global||i.multiline)throw Error(""+i);n.push("(?:"+s(i)+")")}return RegExp(n.join("|"),j?"gi":"g")}function T(a,d){function g(a){var c=a.nodeType;if(c==1){if(!b.test(a.className)){for(c=a.firstChild;c;c=c.nextSibling)g(c);c=a.nodeName.toLowerCase();if("br"===c||"li"===c)s[j]="\n",m[j<<1]=x++,m[j++<<1|1]=a}}else if(c==3||c==4)c=a.nodeValue,c.length&&(c=d?c.replace(/\r\n?/g,"\n"):c.replace(/[\t\n\r ]+/g," "),s[j]=c,m[j<<1]=x,x+=c.length,m[j++<<1|1]=
    a)}var b=/(?:^|\s)nocode(?:\s|$)/,s=[],x=0,m=[],j=0;g(a);return{a:s.join("").replace(/\n$/,""),d:m}}function H(a,d,g,b){d&&(a={a:d,e:a},g(a),b.push.apply(b,a.g))}function U(a){for(var d=void 0,g=a.firstChild;g;g=g.nextSibling)var b=g.nodeType,d=b===1?d?a:g:b===3?V.test(g.nodeValue)?a:d:d;return d===a?void 0:d}function C(a,d){function g(a){for(var j=a.e,k=[j,"pln"],c=0,i=a.a.match(s)||[],r={},n=0,e=i.length;n<e;++n){var z=i[n],w=r[z],t=void 0,f;if(typeof w==="string")f=!1;else{var h=b[z.charAt(0)];
    if(h)t=z.match(h[1]),w=h[0];else{for(f=0;f<x;++f)if(h=d[f],t=z.match(h[1])){w=h[0];break}t||(w="pln")}if((f=w.length>=5&&"lang-"===w.substring(0,5))&&!(t&&typeof t[1]==="string"))f=!1,w="src";f||(r[z]=w)}h=c;c+=z.length;if(f){f=t[1];var l=z.indexOf(f),B=l+f.length;t[2]&&(B=z.length-t[2].length,l=B-f.length);w=w.substring(5);H(j+h,z.substring(0,l),g,k);H(j+h+l,f,I(w,f),k);H(j+h+B,z.substring(B),g,k)}else k.push(j+h,w)}a.g=k}var b={},s;(function(){for(var g=a.concat(d),j=[],k={},c=0,i=g.length;c<i;++c){var r=
    g[c],n=r[3];if(n)for(var e=n.length;--e>=0;)b[n.charAt(e)]=r;r=r[1];n=""+r;k.hasOwnProperty(n)||(j.push(r),k[n]=q)}j.push(/[\S\s]/);s=S(j)})();var x=d.length;return g}function v(a){var d=[],g=[];a.tripleQuotedStrings?d.push(["str",/^(?:'''(?:[^'\\]|\\[\S\s]|''?(?=[^']))*(?:'''|$)|"""(?:[^"\\]|\\[\S\s]|""?(?=[^"]))*(?:"""|$)|'(?:[^'\\]|\\[\S\s])*(?:'|$)|"(?:[^"\\]|\\[\S\s])*(?:"|$))/,q,"'\""]):a.multiLineStrings?d.push(["str",/^(?:'(?:[^'\\]|\\[\S\s])*(?:'|$)|"(?:[^"\\]|\\[\S\s])*(?:"|$)|`(?:[^\\`]|\\[\S\s])*(?:`|$))/,
    q,"'\"`"]):d.push(["str",/^(?:'(?:[^\n\r'\\]|\\.)*(?:'|$)|"(?:[^\n\r"\\]|\\.)*(?:"|$))/,q,"\"'"]);a.verbatimStrings&&g.push(["str",/^@"(?:[^"]|"")*(?:"|$)/,q]);var b=a.hashComments;b&&(a.cStyleComments?(b>1?d.push(["com",/^#(?:##(?:[^#]|#(?!##))*(?:###|$)|.*)/,q,"#"]):d.push(["com",/^#(?:(?:define|e(?:l|nd)if|else|error|ifn?def|include|line|pragma|undef|warning)\b|[^\n\r]*)/,q,"#"]),g.push(["str",/^<(?:(?:(?:\.\.\/)*|\/?)(?:[\w-]+(?:\/[\w-]+)+)?[\w-]+\.h(?:h|pp|\+\+)?|[a-z]\w*)>/,q])):d.push(["com",
    /^#[^\n\r]*/,q,"#"]));a.cStyleComments&&(g.push(["com",/^\/\/[^\n\r]*/,q]),g.push(["com",/^\/\*[\S\s]*?(?:\*\/|$)/,q]));if(b=a.regexLiterals){var s=(b=b>1?"":"\n\r")?".":"[\\S\\s]";g.push(["lang-regex",RegExp("^(?:^^\\.?|[+-]|[!=]=?=?|\\#|%=?|&&?=?|\\(|\\*=?|[+\\-]=|->|\\/=?|::?|<<?=?|>>?>?=?|,|;|\\?|@|\\[|~|{|\\^\\^?=?|\\|\\|?=?|break|case|continue|delete|do|else|finally|instanceof|return|throw|try|typeof)\\s*("+("/(?=[^/*"+b+"])(?:[^/\\x5B\\x5C"+b+"]|\\x5C"+s+"|\\x5B(?:[^\\x5C\\x5D"+b+"]|\\x5C"+
    s+")*(?:\\x5D|$))+/")+")")])}(b=a.types)&&g.push(["typ",b]);b=(""+a.keywords).replace(/^ | $/g,"");b.length&&g.push(["kwd",RegExp("^(?:"+b.replace(/[\s,]+/g,"|")+")\\b"),q]);d.push(["pln",/^\s+/,q," \r\n\t\u00a0"]);b="^.[^\\s\\w.$@'\"`/\\\\]*";a.regexLiterals&&(b+="(?!s*/)");g.push(["lit",/^@[$_a-z][\w$@]*/i,q],["typ",/^(?:[@_]?[A-Z]+[a-z][\w$@]*|\w+_t\b)/,q],["pln",/^[$_a-z][\w$@]*/i,q],["lit",/^(?:0x[\da-f]+|(?:\d(?:_\d+)*\d*(?:\.\d*)?|\.\d\+)(?:e[+-]?\d+)?)[a-z]*/i,q,"0123456789"],["pln",/^\\[\S\s]?/,
    q],["pun",RegExp(b),q]);return C(d,g)}function J(a,d,g){function b(a){var c=a.nodeType;if(c==1&&!x.test(a.className))if("br"===a.nodeName)s(a),a.parentNode&&a.parentNode.removeChild(a);else for(a=a.firstChild;a;a=a.nextSibling)b(a);else if((c==3||c==4)&&g){var d=a.nodeValue,i=d.match(m);if(i)c=d.substring(0,i.index),a.nodeValue=c,(d=d.substring(i.index+i[0].length))&&a.parentNode.insertBefore(j.createTextNode(d),a.nextSibling),s(a),c||a.parentNode.removeChild(a)}}function s(a){function b(a,c){var d=
    c?a.cloneNode(!1):a,e=a.parentNode;if(e){var e=b(e,1),g=a.nextSibling;e.appendChild(d);for(var i=g;i;i=g)g=i.nextSibling,e.appendChild(i)}return d}for(;!a.nextSibling;)if(a=a.parentNode,!a)return;for(var a=b(a.nextSibling,0),d;(d=a.parentNode)&&d.nodeType===1;)a=d;c.push(a)}for(var x=/(?:^|\s)nocode(?:\s|$)/,m=/\r\n?|\n/,j=a.ownerDocument,k=j.createElement("li");a.firstChild;)k.appendChild(a.firstChild);for(var c=[k],i=0;i<c.length;++i)b(c[i]);d===(d|0)&&c[0].setAttribute("value",d);var r=j.createElement("ol");
    r.className="linenums";for(var d=Math.max(0,d-1|0)||0,i=0,n=c.length;i<n;++i)k=c[i],k.className="L"+(i+d)%10,k.firstChild||k.appendChild(j.createTextNode("\u00a0")),r.appendChild(k);a.appendChild(r)}function p(a,d){for(var g=d.length;--g>=0;){var b=d[g];F.hasOwnProperty(b)?D.console&&console.warn("cannot override language handler %s",b):F[b]=a}}function I(a,d){if(!a||!F.hasOwnProperty(a))a=/^\s*</.test(d)?"default-markup":"default-code";return F[a]}function K(a){var d=a.h;try{var g=T(a.c,a.i),b=g.a;
    a.a=b;a.d=g.d;a.e=0;I(d,b)(a);var s=/\bMSIE\s(\d+)/.exec(navigator.userAgent),s=s&&+s[1]<=8,d=/\n/g,x=a.a,m=x.length,g=0,j=a.d,k=j.length,b=0,c=a.g,i=c.length,r=0;c[i]=m;var n,e;for(e=n=0;e<i;)c[e]!==c[e+2]?(c[n++]=c[e++],c[n++]=c[e++]):e+=2;i=n;for(e=n=0;e<i;){for(var p=c[e],w=c[e+1],t=e+2;t+2<=i&&c[t+1]===w;)t+=2;c[n++]=p;c[n++]=w;e=t}c.length=n;var f=a.c,h;if(f)h=f.style.display,f.style.display="none";try{for(;b<k;){var l=j[b+2]||m,B=c[r+2]||m,t=Math.min(l,B),A=j[b+1],G;if(A.nodeType!==1&&(G=x.substring(g,
    t))){s&&(G=G.replace(d,"\r"));A.nodeValue=G;var L=A.ownerDocument,o=L.createElement("span");o.className=c[r+1];var v=A.parentNode;v.replaceChild(o,A);o.appendChild(A);g<l&&(j[b+1]=A=L.createTextNode(x.substring(t,l)),v.insertBefore(A,o.nextSibling))}g=t;g>=l&&(b+=2);g>=B&&(r+=2)}}finally{if(f)f.style.display=h}}catch(u){D.console&&console.log(u&&u.stack||u)}}var D=window,y=["break,continue,do,else,for,if,return,while"],E=[[y,"auto,case,char,const,default,double,enum,extern,float,goto,inline,int,long,register,short,signed,sizeof,static,struct,switch,typedef,union,unsigned,void,volatile"],
    "catch,class,delete,false,import,new,operator,private,protected,public,this,throw,true,try,typeof"],M=[E,"alignof,align_union,asm,axiom,bool,concept,concept_map,const_cast,constexpr,decltype,delegate,dynamic_cast,explicit,export,friend,generic,late_check,mutable,namespace,nullptr,property,reinterpret_cast,static_assert,static_cast,template,typeid,typename,using,virtual,where"],N=[E,"abstract,assert,boolean,byte,extends,final,finally,implements,import,instanceof,interface,null,native,package,strictfp,super,synchronized,throws,transient"],
    O=[N,"as,base,by,checked,decimal,delegate,descending,dynamic,event,fixed,foreach,from,group,implicit,in,internal,into,is,let,lock,object,out,override,orderby,params,partial,readonly,ref,sbyte,sealed,stackalloc,string,select,uint,ulong,unchecked,unsafe,ushort,var,virtual,where"],E=[E,"debugger,eval,export,function,get,null,set,undefined,var,with,Infinity,NaN"],P=[y,"and,as,assert,class,def,del,elif,except,exec,finally,from,global,import,in,is,lambda,nonlocal,not,or,pass,print,raise,try,with,yield,False,True,None"],
    Q=[y,"alias,and,begin,case,class,def,defined,elsif,end,ensure,false,in,module,next,nil,not,or,redo,rescue,retry,self,super,then,true,undef,unless,until,when,yield,BEGIN,END"],W=[y,"as,assert,const,copy,drop,enum,extern,fail,false,fn,impl,let,log,loop,match,mod,move,mut,priv,pub,pure,ref,self,static,struct,true,trait,type,unsafe,use"],y=[y,"case,done,elif,esac,eval,fi,function,in,local,set,then,until"],R=/^(DIR|FILE|vector|(de|priority_)?queue|list|stack|(const_)?iterator|(multi)?(set|map)|bitset|u?(int|float)\d*)\b/,
    V=/\S/,X=v({keywords:[M,O,E,"caller,delete,die,do,dump,elsif,eval,exit,foreach,for,goto,if,import,last,local,my,next,no,our,print,package,redo,require,sub,undef,unless,until,use,wantarray,while,BEGIN,END",P,Q,y],hashComments:!0,cStyleComments:!0,multiLineStrings:!0,regexLiterals:!0}),F={};p(X,["default-code"]);p(C([],[["pln",/^[^<?]+/],["dec",/^<!\w[^>]*(?:>|$)/],["com",/^<\!--[\S\s]*?(?:--\>|$)/],["lang-",/^<\?([\S\s]+?)(?:\?>|$)/],["lang-",/^<%([\S\s]+?)(?:%>|$)/],["pun",/^(?:<[%?]|[%?]>)/],["lang-",
    /^<xmp\b[^>]*>([\S\s]+?)<\/xmp\b[^>]*>/i],["lang-js",/^<script\b[^>]*>([\S\s]*?)(<\/script\b[^>]*>)/i],["lang-css",/^<style\b[^>]*>([\S\s]*?)(<\/style\b[^>]*>)/i],["lang-in.tag",/^(<\/?[a-z][^<>]*>)/i]]),["default-markup","htm","html","mxml","xhtml","xml","xsl"]);p(C([["pln",/^\s+/,q," \t\r\n"],["atv",/^(?:"[^"]*"?|'[^']*'?)/,q,"\"'"]],[["tag",/^^<\/?[a-z](?:[\w-.:]*\w)?|\/?>$/i],["atn",/^(?!style[\s=]|on)[a-z](?:[\w:-]*\w)?/i],["lang-uq.val",/^=\s*([^\s"'>]*(?:[^\s"'/>]|\/(?=\s)))/],["pun",/^[/<->]+/],
    ["lang-js",/^on\w+\s*=\s*"([^"]+)"/i],["lang-js",/^on\w+\s*=\s*'([^']+)'/i],["lang-js",/^on\w+\s*=\s*([^\s"'>]+)/i],["lang-css",/^style\s*=\s*"([^"]+)"/i],["lang-css",/^style\s*=\s*'([^']+)'/i],["lang-css",/^style\s*=\s*([^\s"'>]+)/i]]),["in.tag"]);p(C([],[["atv",/^[\S\s]+/]]),["uq.val"]);p(v({keywords:M,hashComments:!0,cStyleComments:!0,types:R}),["c","cc","cpp","cxx","cyc","m"]);p(v({keywords:"null,true,false"}),["json"]);p(v({keywords:O,hashComments:!0,cStyleComments:!0,verbatimStrings:!0,types:R}),
    ["cs"]);p(v({keywords:N,cStyleComments:!0}),["java"]);p(v({keywords:y,hashComments:!0,multiLineStrings:!0}),["bash","bsh","csh","sh"]);p(v({keywords:P,hashComments:!0,multiLineStrings:!0,tripleQuotedStrings:!0}),["cv","py","python"]);p(v({keywords:"caller,delete,die,do,dump,elsif,eval,exit,foreach,for,goto,if,import,last,local,my,next,no,our,print,package,redo,require,sub,undef,unless,until,use,wantarray,while,BEGIN,END",hashComments:!0,multiLineStrings:!0,regexLiterals:2}),["perl","pl","pm"]);p(v({keywords:Q,
    hashComments:!0,multiLineStrings:!0,regexLiterals:!0}),["rb","ruby"]);p(v({keywords:E,cStyleComments:!0,regexLiterals:!0}),["javascript","js"]);p(v({keywords:"all,and,by,catch,class,else,extends,false,finally,for,if,in,is,isnt,loop,new,no,not,null,of,off,on,or,return,super,then,throw,true,try,unless,until,when,while,yes",hashComments:3,cStyleComments:!0,multilineStrings:!0,tripleQuotedStrings:!0,regexLiterals:!0}),["coffee"]);p(v({keywords:W,cStyleComments:!0,multilineStrings:!0}),["rc","rs","rust"]);
    p(C([],[["str",/^[\S\s]+/]]),["regex"]);var Y=D.PR={createSimpleLexer:C,registerLangHandler:p,sourceDecorator:v,PR_ATTRIB_NAME:"atn",PR_ATTRIB_VALUE:"atv",PR_COMMENT:"com",PR_DECLARATION:"dec",PR_KEYWORD:"kwd",PR_LITERAL:"lit",PR_NOCODE:"nocode",PR_PLAIN:"pln",PR_PUNCTUATION:"pun",PR_SOURCE:"src",PR_STRING:"str",PR_TAG:"tag",PR_TYPE:"typ",prettyPrintOne:D.prettyPrintOne=function(a,d,g){var b=document.createElement("div");b.innerHTML="<pre>"+a+"</pre>";b=b.firstChild;g&&J(b,g,!0);K({h:d,j:g,c:b,i:1});
    return b.innerHTML},prettyPrint:D.prettyPrint=function(a,d){function g(){for(var b=D.PR_SHOULD_USE_CONTINUATION?c.now()+250:Infinity;i<p.length&&c.now()<b;i++){for(var d=p[i],j=h,k=d;k=k.previousSibling;){var m=k.nodeType,o=(m===7||m===8)&&k.nodeValue;if(o?!/^\??prettify\b/.test(o):m!==3||/\S/.test(k.nodeValue))break;if(o){j={};o.replace(/\b(\w+)=([\w%+\-.:]+)/g,function(a,b,c){j[b]=c});break}}k=d.className;if((j!==h||e.test(k))&&!v.test(k)){m=!1;for(o=d.parentNode;o;o=o.parentNode)if(f.test(o.tagName)&&
    o.className&&e.test(o.className)){m=!0;break}if(!m){d.className+=" prettyprinted";m=j.lang;if(!m){var m=k.match(n),y;if(!m&&(y=U(d))&&t.test(y.tagName))m=y.className.match(n);m&&(m=m[1])}if(w.test(d.tagName))o=1;else var o=d.currentStyle,u=s.defaultView,o=(o=o?o.whiteSpace:u&&u.getComputedStyle?u.getComputedStyle(d,q).getPropertyValue("white-space"):0)&&"pre"===o.substring(0,3);u=j.linenums;if(!(u=u==="true"||+u))u=(u=k.match(/\blinenums\b(?::(\d+))?/))?u[1]&&u[1].length?+u[1]:!0:!1;u&&J(d,u,o);r=
    {h:m,c:d,j:u,i:o};K(r)}}}i<p.length?setTimeout(g,250):"function"===typeof a&&a()}for(var b=d||document.body,s=b.ownerDocument||document,b=[b.getElementsByTagName("pre"),b.getElementsByTagName("code"),b.getElementsByTagName("xmp")],p=[],m=0;m<b.length;++m)for(var j=0,k=b[m].length;j<k;++j)p.push(b[m][j]);var b=q,c=Date;c.now||(c={now:function(){return+new Date}});var i=0,r,n=/\blang(?:uage)?-([\w.]+)(?!\S)/,e=/\bprettyprint\b/,v=/\bprettyprinted\b/,w=/pre|xmp/i,t=/^code$/i,f=/^(?:pre|code|xmp)$/i,
    h={};g()}};typeof define==="function"&&define.amd&&define("google-code-prettify",[],function(){return Y})})();}()
```
16. Finally, create the fourth file called "script__LP.js" in the _Assets_ folder and paste the following code inside it:
```js {linenos=table}
/* ===================================================================
 * Imminent 1.0.0 - Main JS
 *
 * ------------------------------------------------------------------- */

(function ($) {
  "use strict";

  const cfg = {
    scrollDuration: 800, // smoothscroll duration
    mailChimpURL:
      "", // mailchimp url
  };
  const $WIN = $(window);

  // Add the User Agent to the <html>
  // will be used for IE10/IE11 detection (Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; Trident/6.0; rv:11.0))
  const doc = document.documentElement;
  doc.setAttribute("data-useragent", navigator.userAgent);

  /* preloader
   * -------------------------------------------------- */
  const ssPreloader = function () {
    $("html").addClass("ss-preload");

    $WIN.on("load", function () {
      // force page scroll position to top at page refresh
      // $('html, body').animate({ scrollTop: 0 }, 'normal');

      // will first fade out the loading animation
      $("#loader").fadeOut("slow", function () {
        // will fade out the whole DIV that covers the website.
        $("#preloader").delay(300).fadeOut("slow");
      });

      // for hero content animations
      $("html").removeClass("ss-preload");
      $("html").addClass("ss-loaded");
    });
  };

  /* pretty print
   * -------------------------------------------------- */
  const ssPrettyPrint = function () {
    $("pre").addClass("prettyprint");
    $(document).ready(function () {
      prettyPrint();
    });
  };

  /* slick slider
   * ------------------------------------------------------ */
  const ssSlickSlider = function () {
    $(".intro-slider").slick({
      arrows: false,
      dots: false,
      autoplay: true,
      autoplaySpeed: 3000,
      fade: true,
      speed: 3000,
    });
  };

  /* modal
   * ---------------------------------------------------- */
  const ssModal = function () {
    const modal = document.querySelector(".modal");
    const trigger = document.querySelector(".modal-trigger");
    const closeButton = document.querySelector(".modal__close");

    function toggleModal() {
      modal.classList.toggle("show-modal");
    }
    function windowOnClick(event) {
      if (event.target === modal) {
        toggleModal();
      }
    }
    function pressEsc(event) {
      if (event.which == "27") {
        modal.classList.remove("show-modal");
      }
    }

    trigger.addEventListener("click", toggleModal);
    closeButton.addEventListener("click", toggleModal);
    window.addEventListener("click", windowOnClick);
    window.addEventListener("keyup", pressEsc);
  };

  /* final countdown
   * ------------------------------------------------------ */
  const ssFinalCountdown = function () {
    const $countdown = $(".counter");
    const countdown = $countdown.data("time") || "";

    const finalDate = countdown;

    $(".counter")
      .countdown(finalDate)
      .on("update.countdown finish.countdown", function (event) {
        const str =
          '<div class="counter__time days">%D&nbsp;<span>D</span></div>' +
          '<div class="counter__time hours">%H&nbsp;<span>H</span></div>' +
          '<div class="counter__time minutes">%M&nbsp;<span>M</span></div>' +
          '<div class="counter__time seconds">%S&nbsp;<span>S</span></div>';

        $(this).html(event.strftime(str));
      });
  };

  /* tabs
   * ---------------------------------------------------- */
  const ssTabs = function () {
    const $tabNavListItems = $("ul.tab-nav__list li");
    const $tabContentItem = $(".tab-content__item");

    $tabContentItem.hide().first().show();

    $tabNavListItems.on("click", function () {
      $tabNavListItems.removeClass("active");
      $(this).addClass("active");
      $tabContentItem.hide();

      const activeTab = $(this).attr("data-id");
      $("#" + activeTab).fadeIn(1000);
    });
  };

  /* alert boxes
   * ------------------------------------------------------ */
  const ssAlertBoxes = function () {
    $(".alert-box").on("click", ".alert-box__close", function () {
      $(this).parent().fadeOut(500);
    });
  };

  /* smooth scrolling
   * ------------------------------------------------------ */
  const ssSmoothScroll = function () {
    $(".smoothscroll").on("click", function (e) {
      const target = this.hash;
      const $target = $(target);

      e.preventDefault();
      e.stopPropagation();

      $("html, body")
        .stop()
        .animate(
          {
            scrollTop: $target.offset().top,
          },
          cfg.scrollDuration,
          "swing"
        )
        .promise()
        .done(function () {
          window.location.hash = target;
        });
    });
  };

  /* back to top
   * ------------------------------------------------------ */
  const ssBackToTop = function () {
    const pxShow = 500;
    const $goTopButton = $(".ss-go-top");

    // Show or hide the button
    if ($(window).scrollTop() >= pxShow)
      $goTopButton.addClass("link-is-visible");

    $(window).on("scroll", function () {
      if ($(window).scrollTop() >= pxShow) {
        if (!$goTopButton.hasClass("link-is-visible"))
          $goTopButton.addClass("link-is-visible");
      } else {
        $goTopButton.removeClass("link-is-visible");
      }
    });
  };

  /* ajaxchimp
   * ------------------------------------------------------ */
  const ssAjaxChimp = function () {
    $("#mc-form").ajaxChimp({
      language: "es",
      url: cfg.mailChimpURL,
    });

    // Mailchimp translation
    //
    //  Defaults:
    //	 'submit': 'Submitting...',
    //  0: 'We have sent you a confirmation email',
    //  1: 'Please enter a value',
    //  2: 'An email address must contain a single @',
    //  3: 'The domain portion of the email address is invalid (the portion after the @: )',
    //  4: 'The username portion of the email address is invalid (the portion before the @: )',
    //  5: 'This email address looks fake or invalid. Please enter a real email address'

    $.ajaxChimp.translations.es = {
      submit: "Submitting...",
      0: '<i class="fas fa-check"></i> We have sent you a confirmation email',
      1: '<i class="fas fa-exclamation-triangle"></i> You must enter a valid e-mail address.',
      2: '<i class="fas fa-exclamation-triangle"></i> E-mail address is not valid.',
      3: '<i class="fas fa-exclamation-triangle"></i> E-mail address is not valid.',
      4: '<i class="fas fa-exclamation-triangle"></i> E-mail address is not valid.',
      5: '<i class="fas fa-exclamation-triangle"></i> E-mail address is not valid.',
    };
  };

  /* initialize
   * ------------------------------------------------------ */
  (function ssInit() {
    ssPreloader();
    ssPrettyPrint();
    ssSlickSlider();
    ssModal();
    ssFinalCountdown();
    ssTabs();
    ssAlertBoxes();
    ssSmoothScroll();
    ssBackToTop();
    ssAjaxChimp();
  })();
})(jQuery);
```

That's it! With this coming soon page, once the store is ready to launch, you’ll have a sizable list of prospective customers who are interested and ready to buy.

Credits: 
This beautiful coming soon page was designed by [Styleshout](https://www.styleshout.com/category-template/coming-soon/) and converted to Shopify by Me. You can find a lot of other coming soon pages design on [Styleshout](https://www.styleshout.com/category-template/coming-soon/) website and if you need help with convert those pages to Shopify don't hesitate to contacting me. See you in the next tutorial
