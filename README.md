# QUIZ MANAGEMENT SYSTEM 
# AUMENTA FEATURE SIRA BAZEIA BA PROFESSOR NIA SUJESTAUN.

Quiz Management System – aumenta feature sira.
Dokumentu ida-ne'e deskreve kona-ba projetu Quiz Management System nian no feature hotu ne'ebe aumenta iha dezenvolvimentu nia laran bazeia ba sujestaun sira ne’ebe Professor.
1. Visão Jeral Projetu
Quiz Management System mak aplikasaun Android ne'ebe dezenvolve ho Kotlin. Aplikasaun ida-ne'e permite administrador sira atu kria, jere, no organiza quiz, no mos permite utilizador (estudante sira) atu responde quiz no haree sira-nia rezultadu. Aplikasaun ida-ne'e uza Firebase Authentication ba jere utilizador sira no Firestore ba base dados.
Tecnolojia importante: Kotlin, Android SDK, Firebase Auth, Firestore, Material Design 3, ZXing QR Code Library.
2. Protesaun Password ba Quiz
Administrador sira bele aumenta password opcional bainhira kria quiz. Bainhira estudante tenta loke quiz ne’ebe protesaun ho password, Kada quiz ida hatudu atu husu password antes quiz komesa. Implementasaun ida-ne'e liu husi:
  - Aumenta 'password' field (String, default mamuk) iha Quiz data model.
  - Aumenta password TextInputLayout iha AdminCreateQuizActivity nia layout
  - Implementa password AlertDialog iha UserDashboardActivity ne'ebe valida password ne'ebe hatama ho password quiz nian ne'ebe rai.
3. Kria  QR Code
Kada quiz ne'ebe iha eziste password no QRCODE atu Evita usario ne’ebe deskonesidu.
  - QrCodeUtil.kt - ZXing library utiliza hodi kria QRCODE bitmap
  - Admin nia lista quiz: kada quiz ne'ebe iha password hatudu botaun QR; bainhira klik, hatudu dialog ho QR code bitmap.
  - User Dashboard: botaun 'Scan QR' (ikon camera) loke camera atu escaneia QR code quiz nian
4. Dark Mode / Apoiu Tema
Aplikasaun suporta tema System (tuir dispositivu), Light, no Dark:
  - ThemeManager.kt - aplika tema ne'ebe hili (AppCompatDelegate.setDefaultNightMode) antes atividade ida nia setContentView
  - PreferencesHelper rai preferensia tema nian.
  - ProfileActivity iha MaterialButtonToggleGroup (System / Light) ba hili tema.
  - Admin Dashboard iha ikon tema (moon/sun) iha kraik 'Welcome back, Admin!' ba muda rapidamente entre Light no Dark
  - values-night/colors.xml define paleta kolor ba modu dark
5. Filter Kategoria ba Quiz
Pajina Admin Manage Quizzes no User Dashboard agora inklui filter dropdown atu ordena quiz tuir kategoria:
  - Kategoria: General Knowledge, Science, Mathematics, History, Geography, Technology, Language, Sports, Entertainment, Business, Education, Other
  - Implementa ho AutoCompleteTextView iha TextInputLayout (endIconMode='dropdown_menu') ho completionThreshold=1
  - Lista kategoria hardcoded hanesan Kotlin constant atu evita problema load resource depois muda tema
6. Pull-to-Refresh (SwipeRefreshLayout)
SwipeRefreshLayout aumenta iha telas importante tolu:
  - Manage Quizzes (admin) - dada ba kraik atu atualiza lista quiz
  - Manage Users (admin) - dada ba kraik atu atualiza lista utilizador
  - User Dashboard - dada ba kraik atu atualiza quiz ne'ebe disponivel
7. Jere Utilizador - Aba Admin/User no Buka
Tela Manage Users hadi'a ho:
  - ChipGroup ho 'Users' no 'Admins' chip atu filter lista utilizador tuir papel
  - Buka TextInputLayout ne'ebe filter utilizador tuir naran ou email iha tempu real
  - FloatingActionButton atu aumenta utilizador foun.
8. Edita Profil
Utilizador sira bele edita sira-nia profil husi tela Profile:
  - Dialogu Edit Name - atualiza naran utilizador nian iha Firestore
  - Dialogu Change Password - presiza password atual ba re-authentication (EmailAuthProvider), depois uza user.updatePassword()
9. Snackbar Feedback no Transisaun Atividade
Hadi'a kualidade UI/UX:
  - DialogUtil.showToast() agora uza Snackbar bainhira iha View context (se lae, uza Toast)
  - Transisaun slide atividade: slide_in_right, slide_out_left (no reversu) aplika globalmente liu husi tema.
  - Layout responsivu: User Dashboard uza ScrollView + SwipeRefreshLayout ho header wrap_content atu suporta rolagem iha landscape
10. Prevensaun Acesso QR Code Fali
Bainhira estudante ida taka ona quiz, escaneia QR code ne’ebe hanesan fali sei la permite atu responde fali. Sistema verifica completedQuizIds husi Firestore antes loke quiz, no hatudu toast: 'Ita boot taka ona quiz ida-ne'e'.
11. Rejistu Utilizador husi Admin
Administrador sira bele kria konta utilizador foun diretamente husi tela Manage Users.
  - Uza Firebase Auth REST API (POST /v1/accounts:signUp) iha fatin createUserWithEmailAndPassword atu mantein sesaun admin nian
  - Depois kria konta Firebase Auth, dokumentu utilizador kria iha Firestore users collection
  - Regra seguransa Firestone atualiza atu permite admin kria dokumentu iha users collection

Resumu
Quiz Management System agora inklui quiz ho protesaun password, kria no escaneia QR code, muda tema dark/light, filter kategoria, pull-to-refresh, jere papel utilizador ho buka, edita profil, Snackbar notifikasaun, transisaun atividade, no layout responsivu ba landscape.

