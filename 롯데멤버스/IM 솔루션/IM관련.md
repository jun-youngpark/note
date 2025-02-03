# IM (통합 계정 관리, Identity Management)

**IM(Identity Management, 통합 계정 관리)**은 기업이나 조직에서 사용자 계정을 **효율적으로 생성, 관리, 보호 및 삭제**하는 프로세스를 의미합니다. 이를 통해 사용자 및 시스템 간 접근 권한을 중앙에서 제어하고 보안성을 강화할 수 있습니다.

---

## 1. IM의 주요 기능

### ① 계정 라이프사이클 관리 (Account Lifecycle Management)
- **사용자 생성 (Provisioning)**: 신규 사용자 계정 자동 생성.
- **사용자 변경 (Modification)**: 직급 변경, 부서 이동 시 계정 정보 업데이트.
- **사용자 삭제 (Deprovisioning)**: 퇴사자 및 비활성 계정 자동 정리.
- **자동화된 계정 관리**: HR 시스템과 연동하여 계정 정보를 자동 반영.

### ② 인증 및 접근 제어 (Authentication & Access Control)
- **싱글 사인온 (SSO, Single Sign-On)**: 한 번 로그인하면 여러 시스템에 자동 로그인.
- **다중 인증 (MFA, Multi-Factor Authentication)**: OTP, 생체 인증 등을 추가하여 보안 강화.
- **권한 관리 (RBAC, Role-Based Access Control)**: 사용자 역할(Role) 기반으로 접근 권한 관리.

### ③ 디렉터리 서비스 연동
- **LDAP 및 Active Directory(AD) 연동**: 기존 디렉터리 서비스와 통합하여 계정 정보 중앙 관리.
- **클라우드 디렉터리 서비스**: Azure AD, Google Workspace 연동.

### ④ 감사 및 로그 관리 (Audit & Compliance)
- **로그인 및 권한 변경 로그 기록**: 내부 보안 감사 및 컴플라이언스 대응.
- **이상 행위 탐지**: 비정상적인 로그인 패턴 감지.
- **규제 준수 지원**: GDPR, HIPAA, ISO 27001 등의 보안 규정 준수.

### ⑤ 비밀번호 관리 (Password Management)
- **비밀번호 정책 설정**: 강력한 비밀번호 생성 요구.
- **비밀번호 재설정 (SSPR, Self-Service Password Reset)**: 사용자가 직접 비밀번호 변경 가능.

---

## 2. IM 솔루션의 필요성

### 🔹 보안 강화
- 비밀번호 공유 및 불필요한 계정 유지 문제 방지.
- MFA 및 SSO를 통한 로그인 보안 강화.

### 🔹 운영 효율성 향상
- 계정 생성 및 폐기 자동화 → IT 부서 업무 부담 감소.
- 모든 시스템에서 **통합 계정 관리** 가능.

### 🔹 규제 및 법률 준수
- **ISO 27001, GDPR, HIPAA** 등 보안 규제 준수를 위한 계정 관리 정책 적용.
- 내부 감사 및 이상 행위 감지 기능 지원.

---

## 3. IM과 관련된 기술 및 프로토콜

### ① 디렉터리 서비스
- **Active Directory (AD)**: Microsoft 환경에서 사용자 계정을 중앙 관리.
- **LDAP (Lightweight Directory Access Protocol)**: 계정 정보를 저장하고 검색하는 표준 프로토콜.

### ② 인증 프로토콜
- **OAuth 2.0**: API 인증 및 권한 부여 프로토콜.
- **OpenID Connect (OIDC)**: OAuth 2.0 기반 사용자 인증 프로토콜.
- **SAML (Security Assertion Markup Language)**: SSO를 지원하는 XML 기반 인증 프로토콜.

### ③ 보안 프레임워크
- **Zero Trust Security**: 네트워크 내부·외부 구분 없이 모든 요청을 검증하는 보안 모델.
- **IAM (Identity & Access Management)**: ID 관리와 접근 제어를 통합 제공.

---

## 4. 주요 IM 솔루션 및 플랫폼

| 솔루션 | 주요 특징 |
|--------|---------|
| **Microsoft Azure AD** | Microsoft 365 및 클라우드 환경에서 ID 및 액세스 관리. SSO, MFA 지원. |
| **Okta** | 클라우드 기반 ID 및 접근 관리(IAM) 솔루션으로 다양한 애플리케이션과 통합 가능. |
| **IBM Security Verify** | AI 기반 ID 및 접근 제어, SSO, MFA 기능 제공. |
| **Ping Identity** | 엔터프라이즈급 IAM 솔루션으로 SSO, MFA, API 보안 제공. |
| **SailPoint IdentityIQ** | ID 거버넌스 및 자동화된 계정 라이프사이클 관리. |
| **OneLogin** | 클라우드 기반 SSO 및 IAM 솔루션, 다양한 SaaS 애플리케이션과 연동 가능. |

---

## 5. IM과 IAM (Identity & Access Management)의 차이

| 비교 항목 | IM (Identity Management) | IAM (Identity & Access Management) |
|-----------|-------------------------|-----------------------------------|
| **초점** | 사용자 계정 및 신원 관리 | 사용자 계정 + 접근 제어까지 포함 |
| **주요 기능** | 사용자 생성, 삭제, 수정, 비밀번호 관리, 감사 | IM 기능 + SSO, MFA, RBAC, 정책 기반 접근 제어 |
| **보안 수준** | 보안의 기초 제공 | 강력한 접근 보안 정책 포함 |
| **예제** | Active Directory, LDAP | Okta, Azure AD, SailPoint |

---

## 6. IM 도입 시 고려할 사항

1. **기업 환경과 호환성**
   - 온프레미스 vs 클라우드 환경 선택.
   - 기존 시스템(AD, ERP, HR 시스템)과의 연동 가능성.

2. **보안 기능**
   - MFA, RBAC(역할 기반 접근 제어), Zero Trust 보안 적용 여부.

3. **규제 준수**
   - GDPR, HIPAA, ISO 27001 등 보안 인증 준수 여부.

4. **확장성**
   - 향후 사용자 증가 및 클라우드, SaaS 환경 확장 지원 여부.

5. **자동화 지원**
   - 계정 생성 및 삭제 자동화, HR 시스템과 연동 기능 제공.

---

## 7. 결론

IM(통합 계정 관리)은 기업의 **보안 강화, 운영 효율성 개선, 규제 준수**를 위해 필수적인 기술입니다. 특히 클라우드 환경 전환이 가속화됨에 따라, IAM(Identity & Access Management) 및 **Zero Trust 보안 모델**과 함께 더욱 중요성이 커지고 있습니다. 적절한 IM 솔루션을 도입하면 **사용자 계정 관리 자동화** 및 **보안 위협 감소**에 큰 도움을 줄 수 있습니다.
