<template>
  <div>
    <header>
      <div class="header-inner container">
        <div class="brand">
          <img :src="logo" alt="Sweet Bliss logo" class="brand-logo" />
          <span class="brand-name">{{ translationsForLang.brandName }}</span>
        </div>
        <nav>
          <ul>
            <li><a href="#" @click.prevent="showPage('home')">{{ translationsForLang.navHome }}</a></li>
            <li><a href="#" @click.prevent="showPage('menu')">{{ translationsForLang.navMenu }}</a></li>
            <li><a href="#" @click.prevent="showPage('contact')">{{ translationsForLang.navContact }}</a></li>
          </ul>
        </nav>
        <div class="lang-dropdown header-lang-dropdown" :class="{ open: langDropdownOpen }">
          <button
            class="lang-toggle"
            type="button"
            aria-haspopup="true"
            :aria-expanded="String(langDropdownOpen)"
            @click="toggleLangDropdown"
          >
            {{ currentLanguage.toUpperCase() }} <i class="fas fa-chevron-down"></i>
          </button>
          <div class="lang-menu">
            <button
              v-for="lang in languageOptions"
              :key="lang"
              class="lang-option"
              :class="{ active: currentLanguage === lang }"
              type="button"
              @click="translatePage(lang)">
              {{ lang.toUpperCase() }}
            </button>
          </div>
        </div>
      </div>
    </header>

    <main>
      <section id="home" class="hero page" :class="{ active: currentPage === 'home' }">
        <div class="hero-left">
          <p class="hero-subtitle">{{ translationsForLang.heroSubtitle }}</p>
          <h1 v-html="translationsForLang.heroHeading"></h1>
          <p class="hero-description">{{ translationsForLang.heroDescription }}</p>
          <div class="hero-buttons">
            <a href="#order" class="hero-button">{{ translationsForLang.orderButton }}</a>
            <button class="hero-button secondary" @click.prevent="showPage('menu')">
              {{ translationsForLang.menuButton }}
            </button>
          </div>
        </div>
        <div class="hero-right">
          <img :src="defaultImage" alt="Sandwich" />
        </div>
      </section>

      <section id="menu" class="menu-page page" :class="{ active: currentPage === 'menu' }">
        <div class="container">
          <button class="back-button" @click="showPage('home')">{{ translationsForLang.backButton }}</button>
          <div class="section-title">
            <span class="section-label">{{ translationsForLang.menuSectionLabel }}</span>
            <h2>{{ translationsForLang.menuSectionTitle }}</h2>
            <p class="section-note">{{ translationsForLang.menuSectionNote }}</p>
          </div>
          <div class="menu-categories">
            <button
              v-for="category in categories"
              :key="category.key"
              class="menu-category"
              :class="{ active: currentMenuCategory === category.key }"
              @click="setActiveMenuCategory(category.key)">
              {{ translationsForLang[category.labelKey] }}
            </button>
          </div>
          <div class="menu-grid">
            <div v-for="item in menuItems" :key="item.nameKey" class="menu-card">
              <img class="menu-card-image" :src="item.image" :alt="translationsForLang[item.nameKey] || ''" />
              <div class="menu-card-body">
                <h3>{{ translationsForLang[item.nameKey] }}</h3>
                <p>{{ translationsForLang[item.descKey] }}</p>
                <div class="menu-card-footer">
                  <span>{{ item.price }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section id="order" class="order-section page" :class="{ active: currentPage === 'order' }">
        <div class="container">
          <div class="order-top">
            <div>
              <p class="small-label">{{ translationsForLang.orderButton }}</p>
              <h2>{{ translationsForLang.orderHeading }}</h2>
            </div>
            <span class="status-pill">{{ translationsForLang.statusPill }}</span>
          </div>
          <div class="order-tabs">
            <button class="tab active">{{ translationsForLang.takeawayTab }}</button>
            <button class="tab">{{ translationsForLang.deliveryTab }}</button>
          </div>
          <div class="order-info">
            <p><i class="fas fa-clock"></i> {{ translationsForLang.pickupTime }} <a href="#">{{ translationsForLang.change }}</a></p>
            <p><i class="fas fa-map-marker-alt"></i> {{ translationsForLang.pickupAddress }}</p>
          </div>
        </div>
      </section>

      <section class="delivery-section page" :class="{ active: currentPage === 'delivery' }">
        <div class="container delivery-inner">
          <div class="delivery-image">
            <img src="https://via.placeholder.com/600x500?text=Takeout+Box" alt="Takeout Box" />
          </div>
          <div class="delivery-text">
            <h2>{{ translationsForLang.deliveryHeading }}</h2>
            <p>{{ translationsForLang.deliveryText }}</p>
            <a href="#order" class="hero-button">{{ translationsForLang.orderButton }}</a>
          </div>
        </div>
      </section>

      <section id="contact" class="footer-hero page" :class="{ active: currentPage === 'contact' }">
        <div class="container footer-hero-inner">
          <img :src="logo" alt="TSP Logo" />
          <div>
            <h2>{{ translationsForLang.contactHeading }}</h2>
            <p>{{ translationsForLang.contactDescription }}</p>
            <div class="footer-details">
              <div>
                <p>{{ translationsForLang.weekdays }}</p>
                <p>{{ translationsForLang.weekendSat }}</p>
                <p>{{ translationsForLang.weekendSun }}</p>
              </div>
              <div>
                <p>Instagram</p>
                <p>Facebook</p>
              </div>
              <div>
                <p>{{ translationsForLang.footerContactEmail }}</p>
                <p>{{ translationsForLang.footerContactPhone }}</p>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>

    <footer class="bottom-footer">
      <div class="container footer-container">
        <div class="footer-column footer-brand">
          <img :src="logo" alt="Sweet Bliss" class="footer-logo" />
          <div>
            <h3>Sweet Bliss</h3>
            <p>{{ translationsForLang.footerBrandDesc }}</p>
          </div>
        </div>

        <div class="footer-column">
          <h4>{{ translationsForLang.footerNavLabel }}</h4>
          <ul class="footer-nav">
            <li><a href="#" @click.prevent="showPage('home')">{{ translationsForLang.footerNavHome }}</a></li>
            <li><a href="#" @click.prevent="showPage('menu')">{{ translationsForLang.footerNavMenu }}</a></li>
            <li><a href="#" @click.prevent="showPage('contact')">{{ translationsForLang.footerNavContact }}</a></li>
          </ul>
        </div>

        <div class="footer-column">
          <h4>{{ translationsForLang.footerContactLabel }}</h4>
          <div class="footer-contact-info">
            <p><a :href="`tel:${translationsForLang.footerContactPhone}`">{{ translationsForLang.footerContactPhone }}</a></p>
            <p><a :href="`mailto:${translationsForLang.footerContactEmail}`">{{ translationsForLang.footerContactEmail }}</a></p>
            <p>{{ translationsForLang.footerAddress }}</p>
          </div>
        </div>

        <div class="footer-column">
          <h4>{{ translationsForLang.footerSocialLabel }}</h4>
          <div class="footer-social">
            <a href="#" class="social-icon" aria-label="Instagram"><i class="fab fa-instagram"></i></a>
            <a href="#" class="social-icon" aria-label="Facebook"><i class="fab fa-facebook-f"></i></a>
            <a href="#" class="social-icon" aria-label="TikTok"><i class="fab fa-tiktok"></i></a>
            <a href="#" class="social-icon" aria-label="Twitter"><i class="fab fa-twitter"></i></a>
          </div>
        </div>
      </div>

      <div class="footer-divider"></div>

      <div class="container footer-bottom">
        <p>{{ translationsForLang.footerCopy }}</p>
        <div class="footer-links">
          <a href="#">{{ translationsForLang.privacy }}</a>
          <a href="#">{{ translationsForLang.terms }}</a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

const logo = new URL('../images/logo.jpg', import.meta.url).href;
const defaultImage = new URL('../images/sandwich.png', import.meta.url).href;

const translations = {
  az: {
    brandName: 'Sweet Bliss',
    navHome: 'Əsas',
    navMenu: 'Menyu',
    navContact: 'Əlaqə',
    heroSubtitle: 'Sendviç Məkanı',
    heroHeading: 'TO<br>SƏNDVİÇ<br>MƏRZ',
    heroDescription: 'Ən yaxşı sendviç, hansı ki, siz heç vaxt dadmamısınız. Heç nə daha çox, heç nə daha az.',
    orderButton: 'Sifariş et',
    menuButton: 'Menyunu göstər',
    menuSectionLabel: 'Bizim Sendviçlər',
    menuSectionTitle: 'Menyu',
    menuSectionNote: 'Biz sizə hələ dadmadığınız ən yaxşı sendviçi təqdim edirik.',
    menuCategoryHotDishes: 'İsti yeməklər',
    menuCategorySandwiches: 'Sendviçlər',
    menuCategorySweets: 'Şirniyyat',
    menuCategoryHotDrinks: 'İsti içkilər',
    menuCategoryColdDrinks: 'Soyuq içkilər',
    backButton: '← Geri',
    orderHeading: 'Nəfis tərkibi evimizdə hazırlanan çörək arasında',
    statusPill: 'Sifariş qəbul edirik',
    takeawayTab: 'Samovyvoz',
    deliveryTab: 'Çatdırılma',
    pickupTime: 'Samovyvoz vaxtı: 30 dəqiqə ərzində',
    change: 'Dəyiş',
    pickupAddress: 'Çatdırılma ünvanı: Bakı, Azərbaycan',
    deliveryHeading: 'Biz çatdırırıq',
    deliveryText: 'İndi sifariş edin və mümkün qədər tez alın.',
    contactHeading: 'Karbohidratlarla hazırlanmışdır',
    contactDescription: 'Nümunəvi küçə 1, Bakı, Azərbaycan',
    weekdays: 'Hə: Cüm: 8:00 - 20:00',
    weekendSat: 'Şə: 9:00 - 19:00',
    weekendSun: 'Bə: 9:00 - 20:00',
    footerSocialLabel: 'Biz sosial şəbəkələrdəyik',
    footerContactEmail: 'info@sweetbliss.ru',
    footerContactPhone: '+7 (123) 456-78-90',
    footerAddress: 'Nümunəvi küçə 1, Bakı, Azərbaycan',
    footerBrandDesc: 'Şəhər sendviç restoranı — təzə reseptlər, sürətli çatdırılma və rahat stil.',
    footerNavLabel: 'Naviqasiya',
    footerNavHome: 'Əsas',
    footerNavMenu: 'Menyu',
    footerNavContact: 'Əlaqə',
    footerCopy: '© 2026 Sweet Bliss. Wix üzərində işlənir.',
    privacy: 'Məxfilik siyasəti',
    terms: 'İstifadə şərtləri',
    menuItemHotDishesName: 'Acılı toyuq bowlu',
    menuItemHotDishesDesc: 'Qril toyuq, qovrulmuş tərəvəzlər, acı sous, düyü bazası.',
    menuItemGrilledChickenFileName: 'Qızardılmış Toyuq Filesi, Fri İlə',
    menuItemGrilledChickenFileDesc: 'Toyuq filesi, duz, istiqat, kartof.',
    menuItemChickenThighsFryName: 'Toyuq Budları, Fri İlə',
    menuItemChickenThighsFryDesc: 'Toyuq budu, duz, istiqat, kartof.',
    menuItemYarpagDolmasiName: 'Yarpağ Dolması',
    menuItemYarpagDolmasiDesc: 'Dana əti, düyü, südst, soğan, üzüm yarpağı, quyruq, duz, istiqat.',
    menuItemEtLangetiFryName: 'Ət Langeti, Fri İlə',
    menuItemEtLangetiFryDesc: 'Toyuq, kartof, duz, istiqat, yağ nəhrə.',
    menuItemToyuqSadaDuyuName: 'Toyuq, Sada Düyü İlə',
    menuItemToyuqSadaDuyuDesc: 'Qızardılmış toyuq, duz, istiqat, nəhra yağı, sada düyü.',
    menuItemToyuqQulayasiName: 'Toyuq Qulayası, Düyü Və Vermişəl İlə',
    menuItemToyuqQulayasiDesc: 'Toyuq Qulayası, düyü, vermişəl, duz, istiqat.',
    menuItemToyuqGrecqaName: 'Toyuq, Qreçka İlə',
    menuItemToyuqGrecqaDesc: 'Toyuq, duz, istiqat, nəhra yağı, qreçka.'
  },
  ru: {
    brandName: 'Sweet Bliss',
    navHome: 'Главная',
    navMenu: 'Меню',
    navContact: 'Контакты',
    heroSubtitle: 'Место Сэндвичей',
    heroHeading: 'ТО<br>СЭНДВИЧ<br>МЕСТО',
    heroDescription: 'Лучший сэндвич, который вы когда-либо пробовали. Ничего больше, ничего меньше.',
    orderButton: 'Заказать',
    menuButton: 'Посмотреть меню',
    menuSectionLabel: 'Наши Сэндвичи',
    menuSectionTitle: 'Меню',
    menuSectionNote: 'Мы делаем только лучший сэндвич, который вы когда-либо пробовали.',
    menuCategoryHotDishes: 'Горячие блюда',
    menuCategorySandwiches: 'Сэндвичи',
    menuCategorySweets: 'Сладости',
    menuCategoryHotDrinks: 'Горячие напитки',
    menuCategoryColdDrinks: 'Холодные напитки',
    backButton: '← Назад',
    orderHeading: 'Невероятные ингредиенты между ломтиками нашего ремесленного хлеба',
    statusPill: 'Принимаем заказы',
    takeawayTab: 'Самовывоз',
    deliveryTab: 'Доставка',
    pickupTime: 'Время самовывоза: До 30 минут',
    change: 'Изменить',
    pickupAddress: 'Адрес самовывоза: Москва, Россия',
    deliveryHeading: 'Мы Доставляем',
    deliveryText: 'Закажите сейчас и получите свой заказ как можно скорее.',
    contactHeading: 'Сделано с углеводами TSP',
    contactDescription: 'ул. Примерная, 1, Москва, Россия',
    weekdays: 'Пн - Пт: 8:00 - 20:00',
    weekendSat: 'Сб: 9:00 - 19:00',
    weekendSun: 'Вс: 9:00 - 20:00',
    footerSocialLabel: 'Мы в соцсетях',
    footerContactEmail: 'info@sweetbliss.ru',
    footerContactPhone: '+7 (123) 456-78-90',
    footerAddress: 'ул. Примерная, 1, Москва, Россия',
    footerBrandDesc: 'Городской ресторан сэндвичей — свежие рецепты, быстрая доставка и уютный стиль.',
    footerNavLabel: 'Навигация',
    footerNavHome: 'Главная',
    footerNavMenu: 'Меню',
    footerNavContact: 'Контакты',
    footerCopy: '© 2026 Sweet Bliss. Работает на Wix.',
    privacy: 'Политика конфиденциальности',
    terms: 'Условия использования',
    menuItemHotDishesName: 'Острый куриный боул',
    menuItemHotDishesDesc: 'Курица на гриле, овощи, острый соус, рисовая основа.',
    menuItemGrilledChickenFileName: 'Жареное куриное филе с фри',
    menuItemGrilledChickenFileDesc: 'Куриное филе, соль, перец, картофель фри.',
    menuItemChickenThighsFryName: 'Куриные бедра с фри',
    menuItemChickenThighsFryDesc: 'Куриная ножка, соль, перец, картофель фри.',
    menuItemYarpagDolmasiName: 'Долма в виноградных листьях',
    menuItemYarpagDolmasiDesc: 'Говяжий фарш, рис, молоко, лук, виноградный лист, курдюк, соль, перец.',
    menuItemEtLangetiFryName: 'Мясной лангет с фри',
    menuItemEtLangetiFryDesc: 'Мясо, картофель, соль, перец, масло.',
    menuItemToyuqSadaDuyuName: 'Курица с простым рисом',
    menuItemToyuqSadaDuyuDesc: 'Жареная курица, соль, перец, растительное масло, простой рис.',
    menuItemToyuqQulayasiName: 'Куриный гуляш с рисом и сметаной',
    menuItemToyuqQulayasiDesc: 'Куриный гуляш, рис, сметана, соль, перец.',
    menuItemToyuqGrecqaName: 'Курица с гречкой',
    menuItemToyuqGrecqaDesc: 'Курица, соль, перец, растительное масло, гречка.'
  },
  en: {
    brandName: 'Sweet Bliss',
    navHome: 'Home',
    navMenu: 'Menu',
    navContact: 'Contact',
    heroSubtitle: 'Sandwich House',
    heroHeading: 'TO<br>SANDWICH<br>SPOT',
    heroDescription: 'The best sandwich you have ever tasted. Nothing more, nothing less.',
    orderButton: 'Order',
    menuButton: 'View Menu',
    menuSectionLabel: 'Our Sandwiches',
    menuSectionTitle: 'Menu',
    menuSectionNote: 'We make only the best sandwich you have ever tried.',
    menuCategoryHotDishes: 'Hot dishes',
    menuCategorySandwiches: 'Sandwiches',
    menuCategorySweets: 'Sweets',
    menuCategoryHotDrinks: 'Hot drinks',
    menuCategoryColdDrinks: 'Cold drinks',
    backButton: '← Back',
    orderHeading: 'Incredible ingredients between slices of our artisan bread',
    statusPill: 'Now taking orders',
    takeawayTab: 'Pickup',
    deliveryTab: 'Delivery',
    pickupTime: 'Pickup time: Up to 30 minutes',
    change: 'Change',
    pickupAddress: 'Pickup address: Moscow, Russia',
    deliveryHeading: 'We Deliver',
    deliveryText: 'Order now and get your meal as soon as possible.',
    contactHeading: 'Made with carbohydrates by TSP',
    contactDescription: 'Sample St, 1, Moscow, Russia',
    weekdays: 'Mon - Fri: 8:00 - 20:00',
    weekendSat: 'Sat: 9:00 - 19:00',
    weekendSun: 'Sun: 9:00 - 20:00',
    footerSocialLabel: 'Find us on socials',
    footerContactEmail: 'info@sweetbliss.ru',
    footerContactPhone: '+7 (123) 456-78-90',
    footerAddress: 'Sample St, 1, Moscow, Russia',
    footerBrandDesc: 'Urban sandwich restaurant — fresh recipes, fast delivery and cozy style.',
    footerNavLabel: 'Navigation',
    footerNavHome: 'Home',
    footerNavMenu: 'Menu',
    footerNavContact: 'Contact',
    footerCopy: '© 2026 Sweet Bliss. Powered by Wix.',
    privacy: 'Privacy Policy',
    terms: 'Terms of Use',
    menuItemHotDishesName: 'Spicy Chicken Bowl',
    menuItemHotDishesDesc: 'Grilled chicken, roasted veggies, spicy sauce, rice base.',
    menuItemGrilledChickenFileName: 'Grilled Chicken Fillet with Fries',
    menuItemGrilledChickenFileDesc: 'Chicken fillet, salt, pepper, fries.',
    menuItemChickenThighsFryName: 'Chicken Thighs with Fries',
    menuItemChickenThighsFryDesc: 'Chicken thigh, salt, pepper, fries.',
    menuItemYarpagDolmasiName: 'Stuffed Grape Leaves',
    menuItemYarpagDolmasiDesc: 'Beef, rice, milk, onion, grape leaf, tail fat, salt, pepper.',
    menuItemEtLangetiFryName: 'Meat Langet with Fries',
    menuItemEtLangetiFryDesc: 'Meat, potatoes, salt, pepper, oil.',
    menuItemToyuqSadaDuyuName: 'Chicken with Plain Rice',
    menuItemToyuqSadaDuyuDesc: 'Grilled chicken, salt, pepper, vegetable oil, plain rice.',
    menuItemToyuqQulayasiName: 'Chicken Goulash with Rice and Cream',
    menuItemToyuqQulayasiDesc: 'Chicken goulash, rice, sour cream, salt, pepper.',
    menuItemToyuqGrecqaName: 'Chicken with Buckwheat',
    menuItemToyuqGrecqaDesc: 'Chicken, salt, pepper, vegetable oil, buckwheat.'
  }
};

const menuItemsByCategory = {
  'hot-dishes': [
    { nameKey: 'menuItemHotDishesName', descKey: 'menuItemHotDishesDesc', price: '599 ₽', image: defaultImage },
    { nameKey: 'menuItemGrilledChickenFileName', descKey: 'menuItemGrilledChickenFileDesc', price: '7,00 AZN', image: defaultImage },
    { nameKey: 'menuItemChickenThighsFryName', descKey: 'menuItemChickenThighsFryDesc', price: '6,00 AZN', image: defaultImage },
    { nameKey: 'menuItemYarpagDolmasiName', descKey: 'menuItemYarpagDolmasiDesc', price: '10,00 AZN', image: defaultImage },
    { nameKey: 'menuItemEtLangetiFryName', descKey: 'menuItemEtLangetiFryDesc', price: '8,00 AZN', image: defaultImage },
    { nameKey: 'menuItemToyuqSadaDuyuName', descKey: 'menuItemToyuqSadaDuyuDesc', price: '8,00 AZN', image: defaultImage },
    { nameKey: 'menuItemToyuqQulayasiName', descKey: 'menuItemToyuqQulayasiDesc', price: '8,50 AZN', image: defaultImage },
    { nameKey: 'menuItemToyuqGrecqaName', descKey: 'menuItemToyuqGrecqaDesc', price: '8,00 AZN', image: defaultImage }
  ],
  sandwiches: [
    { nameKey: 'menuItemSandwichesName', descKey: 'menuItemSandwichesDesc', price: '549 ₽', image: defaultImage }
  ],
  sweets: [
    { nameKey: 'menuItemSweetsName', descKey: 'menuItemSweetsDesc', price: '399 ₽', image: defaultImage }
  ],
  'hot-drinks': [
    { nameKey: 'menuItemHotDrinksName', descKey: 'menuItemHotDrinksDesc', price: '299 ₽', image: defaultImage }
  ],
  'cold-drinks': [
    { nameKey: 'menuItemColdDrinksName', descKey: 'menuItemColdDrinksDesc', price: '279 ₽', image: defaultImage }
  ]
};

const currentLanguage = ref(localStorage.getItem('siteLanguage') || 'az');
const currentMenuCategory = ref('hot-dishes');
const currentPage = ref(localStorage.getItem('currentPage') || 'home');
const langDropdownOpen = ref(false);

const translationsForLang = computed(() => translations[currentLanguage.value] || translations.az);
const menuItems = computed(() => menuItemsByCategory[currentMenuCategory.value] || []);

const languageOptions = ['az', 'ru', 'en'];
const categories = [
  { key: 'hot-dishes', labelKey: 'menuCategoryHotDishes' },
  { key: 'sandwiches', labelKey: 'menuCategorySandwiches' },
  { key: 'sweets', labelKey: 'menuCategorySweets' },
  { key: 'hot-drinks', labelKey: 'menuCategoryHotDrinks' },
  { key: 'cold-drinks', labelKey: 'menuCategoryColdDrinks' }
];

function translatePage(lang) {
  currentLanguage.value = lang;
  langDropdownOpen.value = false;
  localStorage.setItem('siteLanguage', lang);
}

function setActiveMenuCategory(category) {
  currentMenuCategory.value = category;
}

function showPage(page) {
  currentPage.value = page;
  localStorage.setItem('currentPage', page);
}

function toggleLangDropdown() {
  langDropdownOpen.value = !langDropdownOpen.value;
}

onMounted(() => {
  document.documentElement.lang = currentLanguage.value;
});
</script>
