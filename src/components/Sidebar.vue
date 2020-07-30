<template>
  <div>
    <div class="mobile-menu-btn" @click="toggleSideBar()">
      <span class="bar"></span>
      <span class="bar"></span>
      <span class="bar"></span>
    </div>
    <div :class='showSideBar ? "sidebar" : "sidebar mobile-sidebar"'>
      <div class="sidebar_btn-wrapper">
        <div class="sidebar_btn" @click="toggleSideBar()">
          <span class="bar"></span>
          <span class="bar"></span>
          <span class="bar"></span>
        </div>
      </div>

      <div class="sidebar_profile-wrapper">
        <div class="profile">
          <div class="profile_img-wrapper">
            <img :src="profileImage" class="profile_img" />
          </div>
          <span class="profile_name">Aldo Raine</span>
        </div>
      </div>

      <div class="sidebar_menu">
        <div class="sidebar_menu_head">
          <span class="text">Main</span>
          <span class="icon">
            <img :src="downIcon" class="arrow-icon" />
          </span>
        </div>
        <ul class="sidebar_menu_list">
          <li class="sidebar_menu_item">
            <a href="#" class="sidebar_menu_link">
              <div class="sidebar_menu_text">
                <span class="menu-icon">
                  <img :src="menuIcon2" />
                </span>
                <span class="menu-text">Menu Item</span>
              </div>
            </a>
          </li>
          <li class="sidebar_menu_item">
            <a href="#" class="sidebar_menu_link">
              <div class="sidebar_menu_text">
                <span class="menu-icon">
                  <img :src="menuIcon1" />
                </span>
                <span class="menu-text">Menu Item</span>
              </div>
            </a>
          </li>
          <li class="sidebar_menu_item">
            <a href="#" class="sidebar_menu_link">
              <div class="sidebar_menu_text">
                <span class="menu-icon">
                  <img :src="menuIcon3" />
                </span>
                <span class="menu-text">Menu Item</span>
              </div>
              <span class="sidebar_menu_badge">9</span>
            </a>
          </li>
          <li class="sidebar_menu_item">
            <a href="#" class="sidebar_menu_link">
              <div class="sidebar_menu_text">
                <span class="menu-icon">
                  <img :src="menuIcon4" />
                </span>
                <span class="menu-text">Menu Item</span>
              </div>
            </a>
          </li>
        </ul>
      </div>

      <div class="sidebar_menu">
        <div class="sidebar_menu_head">
          <span class="text">Main</span>
          <span class="icon">
            <img :src="downIcon" class="arrow-icon" />
          </span>
        </div>
        <ul class="sidebar_menu_list">
          <li class="sidebar_menu_item">
            <a href="#" class="sidebar_menu_link">
              <div class="sidebar_menu_text">
                <span class="menu-icon">
                  <img :src="menuIcon1" />
                </span>
                <span class="menu-text">Menu Item</span>
              </div>
            </a>
          </li>
          <li class="sidebar_menu_item">
            <a href="#" class="sidebar_menu_link">
              <div class="sidebar_menu_text">
                <span class="menu-icon">
                  <img :src="menuIcon3" />
                </span>
                <span class="menu-text">Menu Item</span>
              </div>
            </a>
          </li>
          <li class="sidebar_menu_item">
            <a href="#" class="sidebar_menu_link">
              <div class="sidebar_menu_text">
                <span class="menu-icon">
                  <img :src="menuIcon2" />
                </span>
                <span class="menu-text">Menu Item</span>
              </div>
            </a>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import profileImage from "../assets/images/profile_img.png";
import menuIcon1 from "../assets/images/menu_icon1.png";
import menuIcon2 from "../assets/images/menu_icon2.png";
import menuIcon3 from "../assets/images/menu_icon3.png";
import menuIcon4 from "../assets/images/menu_icon4.png";
import downIcon from "../assets/images/down_arrow.png";

export default {
  name: "Sidebar",

  components: {

  },

  props: {
  },
  watch: {
 
  },
  data() {
    return {
      profileImage,
      menuIcon1,
      menuIcon2,
      menuIcon3,
      menuIcon4,
      downIcon,
      showSideBar: false
    };
  },
  methods: {
      toggleSideBar: function(){
          this.showSideBar= !this.showSideBar;
      }

  }
};
</script>

<style lang="scss">
@import "../assets/variable.scss";
.sidebar {
  max-width: 340px;
  width: 100%;
  background-color: $blue;
  position: fixed;
  left: 0;
  top: 0;
  bottom: 0;
  height: 100%;
  overflow-y: auto;
  z-index: 999;
  &.mobile-sidebar {
    @media screen and (max-width: 1279px) {
      left: 0 !important;
    }
  }
  &::-webkit-scrollbar-track {
    border-radius: 2;
    background-color: #1b2133;
  }

  &::-webkit-scrollbar {
    width: 1px;
    background-color: #1b2133;
  }

  &::-webkit-scrollbar-thumb {
    border-radius: 2px;
    background-color: #1b2133;
  }
  @media screen and (max-width: 1900px) {
    max-width: 300px;
  }
  @media screen and (max-width: 1599px) {
    max-width: 280px;
  }
  @media screen and (max-width: 1279px) {
    left: -280px;
  }
  &_btn-wrapper {
    border-bottom: 1px solid $darkBlue;
    height: 105px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    @media screen and (max-width: 1599px) {
      height: 88px;
    }
  }
  &_btn {
    width: 32px;
    margin-right: 40px;
    .bar {
      height: 2px;
      width: 100%;
      background-color: $gray;
      margin-bottom: 11px;
      display: block;
      &:last-child {
        margin-bottom: 0;
      }
    }
    @media screen and (max-width: 767px) {
    }
  }
  &_profile-wrapper {
    min-height: 158px;
    display: flex;
    align-items: center;
    border-bottom: 1px solid $darkBlue;
    padding: 0 38px;
    @media screen and (max-width: 1599px) {
      padding: 0 20px;
      min-height: 120px;
    }
    .profile {
      display: flex;
      align-items: center;
      justify-content: space-between;
      &_img-wrapper {
        width: 90px;
        height: 90px;
        border-radius: 50%;
        overflow: hidden;
        @media screen and (max-width: 1599px) {
          width: 70px;
          height: 70px;
        }
        img {
          width: 100%;
          height: 100%;
          object-fit: cover;
        }
      }
      &_name {
        font-size: 28px;
        color: #e4ebf7;
        font-weight: 500;
        display: inline-block;
        margin-left: 25px;
        max-width: 152px;
        line-height: 1.3;
        flex: 1;
        @media screen and (max-width: 1599px) {
          font-size: 22px;
        }
      }
    }
  }
  &_menu {
    border-bottom: 1px solid $darkBlue;
    padding-bottom: 20px;
    &_head {
      height: 62px;
      margin-left: 38px;
      margin-right: 38px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      cursor: pointer;
      .icon {
        width: 17px;
        img {
          width: 100%;
        }
      }
      .text {
        color: $primaryText;
        font-size: 20px;
      }
    }
    &_list {
      margin: 0;
      padding-left: 0;
    }
    &_item {
      height: 65px;
      list-style: none;
    }
    &_badge {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 32px;
      width: 32px;
      color: $gray;
      background-color: #f45b63;
      border-radius: 50%;
      font-size: 18px;
      font-weight: 300;
      @media screen and (max-width: 1599px) {
        height: 25px;
        width: 25px;
        font-size: 16px;
      }
    }
    &_link {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding-left: 38px;
      padding-right: 38px;
      height: 100%;
      font-size: 21px;
      color: $gray;
      text-decoration: none;
      font-weight: 500;
      transition: 0.2s all ease-in-out;
      border-left: 4px solid transparent;
      @media screen and (max-width: 1599px) {
        padding-left: 20px;
        padding-right: 20px;
        font-size: 18px;
      }
      &:hover {
        background-color: $darkBlue;
        border-color: #f45b63;
      }
      .menu-icon {
        margin-right: 10px;
        width: 29px;
        @media screen and (max-width: 1599px) {
          width: 22px;
        }
      }
    }
  }
}
</style>
