<template>
  <div class="sContain PT48 PB165">
    <v-form ref="form" v-model="valid" @submit.prevent="onSubmitForm">
      <div class="signupTitle mb-5">
        회원가입
      </div>
      <div class="signupSubTitle mb-5 d-flex justify-space-around">
        <span class="gray">① 휴대폰 본인확인</span>
        <v-icon color="#d8d8d8">mdi-arrow-right-bold</v-icon>
        <span class="sColor">② 의뢰자 회원가입</span>
      </div>
      <v-text-field
        v-model="userid"
        :rules="useridRules"
        label="아이디"
        required
        outlined
        color="azure"
        hide-details="auto"
        class="MB16"
      />
      <v-text-field
        v-model="password"
        :rules="passwordRules"
        label="비밀번호"
        type="password"
        required
        outlined
        clearable
        color="azure"
        hide-details="auto"
        class="MB16"
      />
      <v-text-field
        v-model="passwordChk"
        :rules="passwordChkRules"
        label="비밀번호 확인"
        type="password"
        required
        outlined
        clearable
        color="azure"
        hide-details="auto"
        class="MB16"
      />
      <v-text-field
        v-model="name"
        outlined
        readonly
        color="azure"
        background-color="grey lighten-2"
        hide-details="auto"
        class="MB16"
      />
      <v-text-field
        v-model="phone"
        outlined
        readonly
        color="azure"
        background-color="grey lighten-2"
        hide-details="auto"
        class="MB16"
      />
      <v-text-field
        v-model="company"
        :rules="companyRules"
        label="기업명(단체명)"
        required
        outlined
        clearable
        color="azure"
        hide-details="auto"
        class="MB16"
      />
      <v-text-field
        v-model="email"
        :rules="emailRules"
        label="이메일"
        required
        outlined
        clearable
        color="azure"
        hide-details="auto"
        class="MB8"
      />
      <div class="d-flex justify-center MB46">
        <div class="grayText">
          <span class="bold">담당자 개인의 이메일 주소</span>로 가입을
          진행해주세요.<br />
          공모전 개최시 회사명을 별도로 입력할 수 있으며,<br />
          담당자의 개인정보는 공개되지 않습니다.
        </div>
      </div>
      <div class="MB16">
        <div class="agreeText">
          로그인/회원가입시<br />
          <span class="underline">이용약관</span>,
          <span class="underline">개인정보처리방침</span>에 동의하게 됩니다.
        </div>
      </div>
      <v-btn :disabled="!valid" class="submitBtn" color="azure" type="submit"
        >동의하고 가입하기</v-btn
      >
    </v-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      valid: false,
      userid: '',
      usertype: 'requester',
      password: '',
      passwordChk: '',
      name: '정윤',
      phone: '01012345678',
      useridRules: [(v) => !!v || '아이디를 입력해주세요.'],
      passwordRules: [(v) => !!v || '비밀번호를 입력해주세요.'],
      passwordChkRules: [
        (v) => !!v || '비밀번호 확인을 입력해주세요.',
        (v) => v === this.password || '비밀번호가 일치하지 않습니다.'
      ],
      companyRules: [(v) => !!v || '기업명(단체명)을 입력해주세요.'],
      emailRules: [
        (v) => !!v || '이메일을 입력해주세요.',
        (v) => /.+@.+/.test(v) || '이메일이 유효하지 않습니다.'
      ]
    }
  },
  methods: {
    onSubmitForm() {
      if (this.$refs.form.validate()) {
        this.$store.dispatch('users/signup', {
          userid: this.userid,
          usertype: this.usertype,
          password: this.password,
          name: this.name,
          phone: this.phone,
          email: this.email,
          company: this.company
        })
      } else {
        alert('폼이 유효하지 않습니다.')
      }
    }
  },
  head() {
    return {
      title: '회원가입'
    }
  },
  middleware: 'anonymous'
}
</script>

<style lang="scss" scoped>
.signupTitle {
  font-family: 'Noto Sans KR', sans-serif;
  font-size: 22px;
  font-weight: bold;
  text-align: center;
}

.signupSubTitle {
  font-family: 'Noto Sans KR', sans-serif;
  font-size: 16px;
  font-weight: bold;
  text-align: center;
}

.gray {
  color: lightGray;
}

.submitBtn {
  width: 100%;
  height: 56px !important;
  color: white;
  font-family: 'Noto Sans KR', sans-serif;
  font-size: 16px;
  font-weight: bold;
}

.grayText {
  font-family: 'Noto Sans KR', sans-serif;
  font-size: 12px;
  color: lightGray;
  .bold {
    font-weight: bold;
  }
}

.agreeText {
  font-family: 'Noto Sans KR', sans-serif;
  font-size: 12px;
  text-align: center;
  .underline {
    text-decoration: underline;
  }
}

.MB8 {
  margin-bottom: 8px;
}

.MB16 {
  margin-bottom: 16px;
}

.MB46 {
  margin-bottom: 46px;
}

.sContain {
  width: 300px;
  left: 0;
  right: 0;
  margin: 0 auto;
}

.sColor {
  color: $azure;
}
</style>
