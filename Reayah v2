import 'package:flutter/material.dart';

void main() {
  runApp(const ParentControlApp());
}

class ParentControlApp extends StatelessWidget {
  const ParentControlApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Parental Control',
      theme: ThemeData.dark().copyWith(
        scaffoldBackgroundColor: const Color(0xFF121212),
        primaryColor: const Color(0xFF00FF66),
        colorScheme: const ColorScheme.dark(
          primary: Color(0xFF00FF66),
          secondary: Color(0xFF00FF66),
          surface: Color(0xFF1E1E1E),
        ),
      ),
      home: const WelcomeLoginScreen(),
    );
  }
}

// -----------------------------------------------------------------------------
// 1. شاشة الدخول الرئيسية (أطفال / ولي الأمر)
// -----------------------------------------------------------------------------
class WelcomeLoginScreen extends StatefulWidget {
  const WelcomeLoginScreen({super.key});

  @override
  State<WelcomeLoginScreen> createState() => _WelcomeLoginScreenState();
}

class _WelcomeLoginScreenState extends State<WelcomeLoginScreen> {
  bool isParentTab = true; // التحكم في التنقل بين الولي والطفل

  // متحكمات النصوص لولي الأمر
  final parentEmailController = TextEditingController();
  final parentPasswordController = TextEditingController();

  // متحكمات النصوص للطفل
  final childEmailController = TextEditingController();
  final childPasswordController = TextEditingController();
  final childParentEmailController = TextEditingController();
  final childParentPasswordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: Padding(
          padding: const EdgeInsets.all(24.0),
          child: Column(
            children: [
              const SizedBox(height: 20),
              // شريط الاختيار العلوي (KIDS / ولي الأمر)
              Container(
                decoration: BoxDecoration(
                  color: const Color(0xFF1E1E1E),
                  borderRadius: BorderRadius.circular(15),
                  border: Border.all(color: Colors.white12),
                ),
                child: Row(
                  children: [
                    Expanded(
                      child: GestureDetector(
                        onTap: () => setState(() => isParentTab = false),
                        child: Container(
                          padding: const EdgeInsets.vertical(14),
                          decoration: BoxDecoration(
                            color: !isParentTab ? const Color(0xFF00FF66) : Colors.transparent,
                            borderRadius: BorderRadius.circular(15),
                          ),
                          child: Center(
                            child: Text(
                              'KIDS',
                              style: TextStyle(
                                fontSize: 18,
                                fontWeight: FontWeight.bold,
                                color: !isParentTab ? Colors.black : Colors.white60,
                              ),
                            ),
                          ),
                        ),
                      ),
                    ),
                    Expanded(
                      child: GestureDetector(
                        onTap: () => setState(() => isParentTab = true),
                        child: Container(
                          padding: const EdgeInsets.vertical(14),
                          decoration: BoxDecoration(
                            color: isParentTab ? const Color(0xFF00FF66) : Colors.transparent,
                            borderRadius: BorderRadius.circular(15),
                          ),
                          child: Center(
                            child: Text(
                              'ولي الأمر',
                              style: TextStyle(
                                fontSize: 18,
                                fontWeight: FontWeight.bold,
                                color: isParentTab ? Colors.black : Colors.white60,
                              ),
                            ),
                          ),
                        ),
                      ),
                    ),
                  ],
                ),
              ),
              const SizedBox(height: 40),

              // محتوى واجهة ولي الأمر أو الطفل
              Expanded(
                child: SingleChildScrollView(
                  child: isParentTab ? _buildParentLoginForm() : _buildKidsSection(),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }

  // نموذج تسجيل دخول ولي الأمر
  Widget _buildParentLoginForm() {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.stretch,
      children: [
        const Text(
          'تسجيل دخول ولي الأمر',
          textAlign: TextAlign.center,
          style: TextStyle(fontSize: 22, fontWeight: FontWeight.bold, color: Colors.white),
        ),
        const SizedBox(height: 30),
        _buildTextField('البريد الإلكتروني', parentEmailController, false, Icons.email),
        const SizedBox(height: 15),
        _buildTextField('كلمة المرور', parentPasswordController, true, Icons.lock),
        const SizedBox(height: 30),
        ElevatedButton(
          style: ElevatedButton.styleFrom(
            backgroundColor: const Color(0xFF00FF66),
            padding: const EdgeInsets.symmetric(vertical: 16),
            shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
          ),
          onPressed: () {
            Navigator.pushReplacement(
              context,
              MaterialPageRoute(builder: (context) => const ParentDashboard()),
            );
          },
          child: const Text('دخول ولي الأمر', style: TextStyle(color: Colors.black, fontSize: 18, fontWeight: FontWeight.bold)),
        ),
      ],
    );
  }

  // قسم الأطفال (الرسالة والتنبيه قبل إظهار الخيارات)
  Widget _buildKidsSection() {
    return Column(
      children: [
        Container(
          padding: const EdgeInsets.all(20),
          decoration: BoxDecoration(
            color: const Color(0xFF1E1E1E),
            borderRadius: BorderRadius.circular(15),
            border: Border.all(color: const Color(0xFF00FF66).withOpacity(0.3)),
          ),
          child: Column(
            children: [
              const Icon(Icons.info_outline, color: Color(0xFF00FF66), size: 48),
              const SizedBox(height: 15),
              const Text(
                'يرجى إعطاء الهاتف لولي الأمر لمتابعة التسجيل',
                textAlign: TextAlign.center,
                style: TextStyle(fontSize: 18, color: Colors.white, height: 1.4),
              ),
              const SizedBox(height: 20),
              ElevatedButton(
                style: ElevatedButton.styleFrom(
                  backgroundColor: const Color(0xFF00FF66),
                  minimumSize: const Size(double.infinity, 45),
                  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
                ),
                onPressed: () {
                  _showKidsLoginDialog();
                },
                child: const Text('حسناً', style: TextStyle(color: Colors.black, fontSize: 16, fontWeight: FontWeight.bold)),
              ),
            ],
          ),
        ),
      ],
    );
  }

  // نافذة إدخال بيانات الطفل وولي الأمر بعد ضغط "حسناً"
  void _showKidsLoginDialog() {
    showModalBottomSheet(
      context: context,
      isScrollControlled: true,
      backgroundColor: const Color(0xFF121212),
      shape: const RoundedRectangleBorder(
        borderRadius: BorderRadius.vertical(top: Radius.circular(25)),
      ),
      builder: (context) {
        return Padding(
          padding: EdgeInsets.only(
            bottom: MediaQuery.of(context).viewInsets.bottom + 20,
            top: 20,
            left: 20,
            right: 20,
          ),
          child: SingleChildScrollView(
            child: Column(
              mainAxisSize: MainAxisSize.min,
              crossAxisAlignment: CrossAxisAlignment.stretch,
              children: [
                const Text(
                  'بيانات ربط حساب الطفل',
                  textAlign: TextAlign.center,
                  style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold, color: Color(0xFF00FF66)),
                ),
                const SizedBox(height: 20),
                _buildTextField('البريد الإلكتروني للطفل', childEmailController, false, Icons.person),
                const SizedBox(height: 10),
                _buildTextField('كلمة سر الطفل', childPasswordController, true, Icons.lock_outline),
                const SizedBox(height: 10),
                _buildTextField('البريد الإلكتروني لولي الأمر', childParentEmailController, false, Icons.mark_as_unread),
                const SizedBox(height: 10),
                _buildTextField('كلمة سر ولي الأمر', childParentPasswordController, true, Icons.security),
                const SizedBox(height: 20),
                ElevatedButton(
                  style: ElevatedButton.styleFrom(
                    backgroundColor: const Color(0xFF00FF66),
                    padding: const EdgeInsets.symmetric(vertical: 14),
                    shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
                  ),
                  onPressed: () {
                    Navigator.pop(context);
                    Navigator.pushReplacement(
                      context,
                      MaterialPageRoute(builder: (context) => const ChildDashboard()),
                    );
                  },
                  child: const Text('تسجيل ودخول', style: TextStyle(color: Colors.black, fontSize: 16, fontWeight: FontWeight.bold)),
                ),
              ],
            ),
          ),
        );
      },
    );
  }

  Widget _buildTextField(String label, TextEditingController controller, bool isPassword, IconData icon) {
    return TextField(
      controller: controller,
      obscureText: isPassword,
      style: const TextStyle(color: Colors.white),
      decoration: InputDecoration(
        prefixIcon: Icon(icon, color: const Color(0xFF00FF66)),
        labelText: label,
        labelStyle: const TextStyle(color: Colors.white60),
        filled: true,
        fillColor: const Color(0xFF1E1E1E),
        enabledBorder: OutlineInputBorder(
          borderRadius: BorderRadius.circular(12),
          borderSide: const BorderSide(color: Colors.white10),
        ),
        focusedBorder: OutlineInputBorder(
          borderRadius: BorderRadius.circular(12),
          borderSide: const BorderSide(color: Color(0xFF00FF66)),
        ),
      ),
    );
  }
}

// -----------------------------------------------------------------------------
// 2. لوحة تحكم ولي الأمر (Parent Dashboard)
// -----------------------------------------------------------------------------
class ParentDashboard extends StatefulWidget {
  const ParentDashboard({super.key});

  @override
  State<ParentDashboard> createState() => _ParentDashboardState();
}

class _ParentDashboardState extends State<ParentDashboard> {
  bool isConnected = false;
  bool isPhoneLocked = false;
  final TextEditingController notificationController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('لوحة تحكم الولي', style: TextStyle(color: Colors.white)),
        backgroundColor: const Color(0xFF1E1E1E),
        actions: [
          IconButton(
            icon: const Icon(Icons.logout, color: Colors.redAccent),
            onPressed: () => Navigator.pushReplacement(
              context,
              MaterialPageRoute(builder: (context) => const WelcomeLoginScreen()),
            ),
          )
        ],
      ),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: SingleChildScrollView(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: [
              // زر الربط بجوال الطفل
              ElevatedButton.icon(
                style: ElevatedButton.styleFrom(
                  backgroundColor: isConnected ? Colors.grey[800] : const Color(0xFF00FF66),
                  padding: const EdgeInsets.vertical(16),
                  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
                ),
                icon: Icon(
                  isConnected ? Icons.phonelink_ring : Icons.phonelink_setup,
                  color: isConnected ? const Color(0xFF00FF66) : Colors.black,
                ),
                label: Text(
                  isConnected ? 'الجهازان متصلان الآن' : 'اتصال بجوال الطفل',
                  style: TextStyle(
                    color: isConnected ? Colors.white : Colors.black,
                    fontSize: 18,
                    fontWeight: FontWeight.bold,
                  ),
                ),
                onPressed: () {
                  setState(() {
                    isConnected = !isConnected;
                  });
                },
              ),
              const SizedBox(height: 25),

              if (isConnected) ...[
                // زر إيقاف وفك إيقاف جوال الطفل
                Container(
                  padding: const EdgeInsets.all(16),
                  decoration: BoxDecoration(
                    color: const Color(0xFF1E1E1E),
                    borderRadius: BorderRadius.circular(15),
                    border: Border.all(color: isPhoneLocked ? Colors.red : const Color(0xFF00FF66)),
                  ),
                  child: Column(
                    children: [
                      Text(
                        isPhoneLocked ? 'حالة الجهاز: مفرزن (مغلق)' : 'حالة الجهاز: يعمل بشكل طبيعي',
                        style: TextStyle(
                          fontSize: 16,
                          fontWeight: FontWeight.bold,
                          color: isPhoneLocked ? Colors.red : const Color(0xFF00FF66),
                        ),
                      ),
                      const SizedBox(height: 15),
                      ElevatedButton(
                        style: ElevatedButton.styleFrom(
                          backgroundColor: isPhoneLocked ? const Color(0xFF00FF66) : Colors.red,
                          minimumSize: const Size(double.infinity, 50),
                          shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
                        ),
                        onPressed: () {
                          setState(() {
                            isPhoneLocked = !isPhoneLocked;
                          });
                        },
                        child: Text(
                          isPhoneLocked ? 'فك تجميد الهاتف' : 'تجميد (إيقاف) هاتف الطفل',
                          style: TextStyle(
                            color: isPhoneLocked ? Colors.black : Colors.white,
                            fontSize: 16,
                            fontWeight: FontWeight.bold,
                          ),
                        ),
                      ),
                    ],
                  ),
                ),
                const SizedBox(height: 25),

                // إرسال إشعار لكلمة معينة
                Container(
                  padding: const EdgeInsets.all(16),
                  decoration: BoxDecoration(
                    color: const Color(0xFF1E1E1E),
                    borderRadius: BorderRadius.circular(15),
                  ),
                  child: Column(
                    crossAxisAlignment: CrossAxisAlignment.stretch,
                    children: [
                      const Text('إرسال تنبيه للهاتف', style: TextStyle(fontSize: 16, color: Colors.white)),
                      const SizedBox(height: 10),
                      TextField(
                        controller: notificationController,
                        style: const TextStyle(color: Colors.white),
                        decoration: InputDecoration(
                          hintText: 'اكتب الكلمة هنا...',
                          hintStyle: const TextStyle(color: Colors.white38),
                          filled: true,
                          fillColor: const Color(0xFF121212),
                          border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(10),
                            borderSide: BorderSide.none,
                          ),
                        ),
                      ),
                      const SizedBox(height: 10),
                      ElevatedButton.icon(
                        style: ElevatedButton.styleFrom(
                          backgroundColor: const Color(0xFF00FF66),
                          shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
                        ),
                        icon: const Icon(Icons.send, color: Colors.black),
                        label: const Text('إرسال الكلمة لجوال الطفل', style: TextStyle(color: Colors.black, fontWeight: FontWeight.bold)),
                        onPressed: () {
                          if (notificationController.text.isNotEmpty) {
                            ScaffoldMessenger.of(context).showSnackBar(
                              SnackBar(content: Text('تم إرسال: "${notificationController.text}" بنجاح')),
                            );
                            notificationController.clear();
                          }
                        },
                      ),
                    ],
                  ),
                ),
                const SizedBox(height: 25),

                // زر بث ومراقبة الشاشة
                ElevatedButton.icon(
                  style: ElevatedButton.styleFrom(
                    backgroundColor: const Color(0xFF1E1E1E),
                    padding: const EdgeInsets.vertical(16),
                    side: const BorderSide(color: Color(0xFF00FF66)),
                    shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
                  ),
                  icon: const Icon(Icons.screen_share, color: Color(0xFF00FF66)),
                  label: const Text('عرض شاشة جوال الطفل بث مباشر', style: TextStyle(color: Color(0xFF00FF66), fontSize: 16, fontWeight: FontWeight.bold)),
                  onPressed: () {
                    Navigator.push(
                      context,
                      MaterialPageRoute(builder: (context) => const ChildScreenViewer()),
                    );
                  },
                ),
              ],
            ],
          ),
        ),
      ),
    );
  }
}

// -----------------------------------------------------------------------------
// 3. شاشة بث شاشة الطفل لولي الأمر
// -----------------------------------------------------------------------------
class ChildScreenViewer extends StatelessWidget {
  const ChildScreenViewer({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('بث شاشة جوال الطفل'),
        backgroundColor: const Color(0xFF1E1E1E),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Container(
              width: 250,
              height: 500,
              decoration: BoxDecoration(
                color: Colors.black,
                borderRadius: BorderRadius.circular(25),
                border: Border.all(color: const Color(0xFF00FF66), width: 4),
              ),
              child: const Center(
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    Icon(Icons.live_tv, color: Color(0xFF00FF66), size: 50),
                    SizedBox(height: 10),
                    Text('جاري عرض شاشة الطفل...', style: TextStyle(color: Colors.white70)),
                  ],
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}

// -----------------------------------------------------------------------------
// 4. واجهة جهاز الطفل (Child Dashboard)
// -----------------------------------------------------------------------------
class ChildDashboard extends StatelessWidget {
  const ChildDashboard({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('تطبيق الطفل'),
        backgroundColor: const Color(0xFF1E1E1E),
        automaticallyImplyLeading: false,
      ),
      body: Center(
        child: Padding(
          padding: const EdgeInsets.all(20.0),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              const Icon(Icons.check_circle_outline, color: Color(0xFF00FF66), size: 80),
              const SizedBox(height: 20),
              const Text(
                'الجهاز متصل بحساب ولي الأمر',
                style: TextStyle(fontSize: 20, color: Colors.white, fontWeight: FontWeight.bold),
              ),
              const SizedBox(height: 10),
              const Text(
                'يمكنك استخدام كافة التطبيقات بحرية طالما الجهاز مسموح به.',
                textAlign: TextAlign.center,
                style: TextStyle(color: Colors.white60),
              ),
            ],
          ),
        ),
      ),
    );
  }
}