<template>
  <div
    v-if="isOpen"
    class="dropdown"
    role="dialog"
    aria-modal="true"
    :aria-hidden="!isOpen"
    @keydown.esc="closeDropdown"
  >
    <transition name="dropdown" appear>
      <div class="dropdown__content">
        <nav class="nav" aria-label="Основное меню">
          <ul class="nav__list">
            <li>
              <NuxtLink to="/#about" @click="closeDropdown"> О нас </NuxtLink>
            </li>
            <li>
              <NuxtLink to="/#catalog" @click="closeDropdown">
                Каталог авто
              </NuxtLink>
            </li>
          </ul>
        </nav>

        <div class="contacts">
          <WhatsApp />
          <Telegram />

          <a
            href="tel:+79309993344"
            class="contacts__link--phone"
            aria-label="Позвонить по номеру +7 930 999-33-44"
          >
            +7-930-999-33-44
          </a>
        </div>
      </div>
    </transition>
    <div class="dropdown__overlay" @click="closeDropdown" aria-hidden="true" />
  </div>
</template>

<script setup>
import Telegram from '@/components/ui/links/Telegram.vue'
import WhatsApp from '@/components/ui/links/WhatsApp.vue'

const props = defineProps({
  isOpen: Boolean,
})

const emit = defineEmits(['close'])

const closeDropdown = () => emit('close')
</script>

<style scoped lang="scss">
.dropdown {
  width: 100%;
  font-weight: 600;
  font-size: 1.25rem;

  @include tablet {
    display: none;
  }
  &__overlay {
    position: fixed;
    inset: 60px 0 0 0;
    z-index: -1;
    background-color: rgba(0, 0, 0, 0.5);
  }

  &__content {
    background: white;
    box-shadow: 0px 10px 10px 0px rgba(15, 16, 17, 0.1);
    padding: 20px;
  }
}

.contacts {
  display: flex;
  align-items: center;
  gap: 16px;
  padding-top: 16px;
  border-top: 1px solid #eee;

  &__link {
    &--phone {
      margin-left: auto;
    }
  }
}

.nav {
  margin-bottom: 24px;
  &__list {
    flex-direction: column;
    gap: 16px;
  }
}

.dropdown-enter-active,
.dropdown-leave-active {
  transition: all 0.3s ease;
}

.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
