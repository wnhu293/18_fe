<template>
    <header>
        <div class="topbar d-flex align-items-center">
            <nav class="navbar navbar-expand">
                <div class="topbar-logo-header d-flex align-items-center">
                    <img src="https://dzfullstack.com/assets/images/logo-img.png" class="logo-icon" style="width: 70px;"
                        alt="logo icon">
                    <h4 class="mt-3 ms-2">DZFULLSTACK</h4>
                </div>
                <div class="mobile-toggle-menu"><i class='bx bx-menu'></i></div>
                <div class="search-bar flex-grow-1">
                    <div class="position-relative search-bar-box input-group w-100">
                        <input type="text"
                            class="form-control search-control border border-1 border-secondary radius-30"
                            placeholder="Search..."> <span
                            class="position-absolute top-50 search-show translate-middle-y"><i
                                class='bx bx-search'></i></span>
                        <span class="position-absolute top-50 search-close translate-middle-y"><i
                                class='bx bx-x'></i></span>
                        <button class="btn btn-outline-secondary radius-30" type="button" id="button-addon2">Tìm
                            Kiếm</button>
                    </div>
                </div>
                <template v-if="auth">
                    <div class="top-menu ms-3">
                        <ul class="navbar-nav align-items-center">
                            <li class="nav-item mobile-search-icon">
                                <a class="nav-link" href="#"> <i class='bx bx-search'></i>
                                </a>
                            </li>
                            <li class="nav-item dropdown dropdown-large">
                                <router-link to="/khach-hang/gio-hang">
                                    <a class="nav-link position-relative"> <span class="alert-count">7</span>
                                        <i class='bx bx-cart-alt'></i>
                                    </a>
                                </router-link>
                            </li>
                        </ul>
                    </div>
                    <div class="user-box dropdown">
                        <a class="d-flex align-items-center nav-link dropdown-toggle dropdown-toggle-nocaret" href="#"
                            role="button" data-bs-toggle="dropdown" aria-expanded="false">
                            <img src="../../assets/images/avatars/avatar-2.png" class="user-img" alt="user avatar">
                            <div class="user-info ps-3">
                                <p class="user-name mb-0">{{ name_kh }}</p>
                                <p class="designattion mb-0">Khách Hàng</p>
                            </div>
                        </a>
                        <ul class="dropdown-menu dropdown-menu-end">
                            <li>
                                <router-link to="/khach-hang/profile">
                                    <a class="dropdown-item" href="javascript:;">
                                        <i class="bx bx-user"></i><span>Profile</span>
                                    </a>
                                </router-link>
                            </li>
                            <li>
                                <div class="dropdown-divider mb-0"></div>
                            </li>
                            <li><a class="dropdown-item"><i class='bx bx-log-out-circle'></i><span>Đăng
                                        Xuất</span></a>
                            </li>
                            <li><a class="dropdown-item"><i class='bx bx-log-out-circle'></i><span>Đăng Xuất Tất
                                        Cả</span></a>
                            </li>
                        </ul>
                    </div>
                </template>
                <template v-else>
                    <div class="user-box dropdown">
                        <router-link to="/khach-hang/dang-nhap">
                            <button type="button"
                                class="btn btn-outline-dark px-5 radius-30 me-2 d-flex align-items-center"><i
                                    class="fa-regular fa-user me-2"></i>Đăng Nhập</button>
                        </router-link>
                        <router-link to="/khach-hang/dang-ky">
                            <button type="button" class="btn btn-dark px-5 radius-30 d-flex align-items-center"><i
                                    class="fa-solid fa-arrow-right-to-bracket me-2"></i>Đăng Ký</button>
                        </router-link>
                    </div>
                </template>
            </nav>
        </div>
    </header>
</template>
<script>
import axios from 'axios';
export default {
    data() {
        return {
            auth: false,
            name_kh: '',
        }
    },
    mounted() {
        this.checkLogin();
        this.name_kh = localStorage.getItem('ten_kh')
    },
    methods: {
        checkLogin() {
            axios
                .get('http://127.0.0.1:8000/api/kiem-tra-khachhang', {
                    headers: {
                        Authorization: 'Bearer ' + localStorage.getItem("token_khach_hang")
                    }
                })
                .then((res) => {
                    if (res.data.status) {
                        this.auth = true
                    } else {
                        var thong_bao = '<b>Thông báo</b><span style="margin-top: 5px">' + res.data.message + '<span>';
                        this.$toast.error(thong_bao);
                    }
                })
        },
    },
}
</script>
<style></style>