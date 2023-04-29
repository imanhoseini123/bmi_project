// ignore_for_file: sized_box_for_whitespace

import 'package:flutter/material.dart';

class MyForm extends StatefulWidget {
  const MyForm({super.key});

  @override
  State<MyForm> createState() => _MyFormState();
}

class _MyFormState extends State<MyForm> {
  double slidernum = 25;
  final _controller = TextEditingController();
  final _controller2 = TextEditingController();
  String textcontroll = '';
  String textcontroll2 = '';

  String bmi = '';
  String name = '';
  num group = 1;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: const Color.fromARGB(137, 36, 35, 35),
      body: SafeArea(
        child: SingleChildScrollView(
          child: Center(
            child: Column(
              children: <Widget>[
                const SizedBox(height: 10),
                const Text(
                  'BMI  Calculator',
                  style: TextStyle(
                    color: Colors.yellow,
                    fontSize: 20,
                    fontWeight: FontWeight.bold,
                  ),
                ),
                const SizedBox(height: 10),
                const SizedBox(width: 10),
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  crossAxisAlignment: CrossAxisAlignment.center,
                  children: [
                    const SizedBox(width: 10),
                    // ignore: sized_box_for_whitespace
                    Container(
                      width: 130,
                      child: textflid2(),
                    ),
                    const SizedBox(width: 100),
                    Padding(
                      padding: const EdgeInsets.only(right: 15.0),
                      child: Container(
                        width: 130,
                        child: TextFormField(
                          autovalidateMode: AutovalidateMode.always,
                          controller: _controller2,
                          keyboardType: TextInputType.number,
                          textDirection: TextDirection.rtl,
                          decoration: const InputDecoration(
                            hintText: 'وزن(kg)',
                            hintTextDirection: TextDirection.rtl,
                            helperText: 'وزن',
                            hoverColor: Colors.yellow,
                            helperStyle: TextStyle(
                              color: Colors.white,
                            ),
                            disabledBorder: InputBorder.none,
                            enabledBorder: InputBorder.none,
                            hintStyle: TextStyle(
                              fontFamily: 'Vazir',
                              color: Colors.white,
                              fontSize: 30,
                              fontWeight: FontWeight.w300,
                            ),
                          ),
                          style: const TextStyle(
                            color: Colors.yellow,
                            fontSize: 40,
                            fontWeight: FontWeight.w300,
                          ),
                          validator: (String? value) {
                            if (value!.isEmpty) {
                              return 'این فیلد را باید پر کنید';
                            }
                            if (value.length < 2) {
                              return 'وزن را درست وارد کنید';
                            }
                            if (double.parse(_controller2.text) >= 300) {
                              _controller2.text = '';
                            }
                          },
                        ),
                      ),
                    ),
                  ],
                ),
                const SizedBox(height: 20),
                Row(
                  children: <Widget>[
                    const SizedBox(width: 50),
                    Column(
                      children: [
                        const Text(
                          'برحسب سانتی متر',
                          style: TextStyle(
                            color: Colors.white,
                            fontSize: 20,
                            fontFamily: 'Vazir',
                          ),
                        ),
                        Radio(
                          value: 1,
                          groupValue: group,
                          onChanged: (num? value) {
                            setState(() {
                              group = value!;
                            });
                          },
                        ),
                      ],
                    ),
                    const SizedBox(width: 50),
                    Column(
                      children: [
                        const Text(
                          'برحسب اینچ',
                          style: TextStyle(
                            color: Colors.white,
                            fontSize: 20,
                            fontFamily: 'Vazir',
                          ),
                        ),
                        Radio(
                          value: 2,
                          groupValue: group,
                          onChanged: (num? value) {
                            setState(() {
                              group = value!;
                            });
                          },
                        ),
                      ],
                    ),
                  ],
                ),
                TextButton(
                  onPressed: () {
                    if (group == 1) {
                      textcontroll = _controller.text;
                      textcontroll2 = _controller2.text;
                      double double1 = double.parse(textcontroll);
                      double double2 = double.parse(textcontroll2);

                      setState(() {
                        if (double2 > 20 && double1 > 140) {
                          if (double2 < 230 && double1 < 210) {
                            double zarb = (double1 / 100 * double1 / 100);
                            double math = double2 / zarb;
                            String value() {
                              if (math < 18) {
                                return 'وزنت کمه';
                              } else if (math <= 25 && math >= 18) {
                                return 'وزنت عالیه';
                              } else if (math < 29.9 && math > 25) {
                                return 'اضافه وزن داری';
                              } else if (math < 34.9 && math >= 30) {
                                return 'چاقی';
                              } else {
                                return 'خیلی چاقی';
                              }
                            }

                            bmi = double.parse((math).toStringAsFixed(2))
                                .toString();
                            slidernum = math;
                            name = value();
                          } else {
                            _controller.text = '';
                            _controller2.text = '';

                            ScaffoldMessenger.of(context).showSnackBar(SnackBar(
                              content: const Text(
                                'لطفا اطلاعات را درست وارد کنید',
                                textDirection: TextDirection.rtl,
                              ),
                              duration: const Duration(seconds: 4),
                              action: SnackBarAction(
                                label: 'متوجه شدم',
                                onPressed: () {},
                              ),
                            ));
                          }
                        } else {
                          _controller.text = '';
                          _controller2.text = '';

                          ScaffoldMessenger.of(context).showSnackBar(SnackBar(
                            content: const Text(
                              'لطفا اطلاعات را درست وارد کنید',
                              textDirection: TextDirection.rtl,
                            ),
                            duration: const Duration(seconds: 4),
                            action: SnackBarAction(
                              label: 'متوجه شدم',
                              onPressed: () {},
                            ),
                          ));
                        }
                      });
                    }
                    if (group == 2) {
                      textcontroll = _controller.text;
                      textcontroll2 = _controller2.text;
                      double double1 = double.parse(textcontroll);
                      double double2 = double.parse(textcontroll2);

                      setState(() {
                        if (double2 > 20 && double1 > 30) {
                          if (double2 < 230 && double1 < 160) {
                            double cm = double1 * 2.5;
                            double zarb = (cm / 100 * cm / 100);
                            double math = (double2 / zarb);
                            String value() {
                              if (math < 18) {
                                return 'وزنت کمه';
                              } else if (math <= 25 && math >= 18) {
                                return 'وزنت عالیه';
                              } else if (math < 29.9 && math > 25) {
                                return 'اضافه وزن داری';
                              } else if (math < 34.9 && math >= 30) {
                                return 'چاقی';
                              } else {
                                return 'خیلی چاقی';
                              }
                            }

                            bmi = double.parse((math).toStringAsFixed(2))
                                .toString();
                            slidernum = math;
                            name = value();
                          } else {
                            _controller.text = '';
                            _controller2.text = '';

                            ScaffoldMessenger.of(context).showSnackBar(SnackBar(
                              content: const Text(
                                'لطفا اطلاعات را درست وارد کنید',
                                textDirection: TextDirection.rtl,
                              ),
                              duration: const Duration(seconds: 4),
                              action: SnackBarAction(
                                label: 'متوجه شدم',
                                onPressed: () {},
                              ),
                            ));
                          }
                        } else {
                          _controller.text = '';
                          _controller2.text = '';

                          ScaffoldMessenger.of(context).showSnackBar(SnackBar(
                            content: const Text(
                              'لطفا اطلاعات را درست وارد کنید',
                              textDirection: TextDirection.rtl,
                            ),
                            duration: const Duration(seconds: 4),
                            action: SnackBarAction(
                              label: 'متوجه شدم',
                              onPressed: () {},
                            ),
                          ));
                        }
                      });
                    }
                  },
                  style: TextButton.styleFrom(
                    foregroundColor: Colors.yellow,
                  ),
                  child: const Text(
                    'محسابه',
                    style: TextStyle(
                      fontSize: 30,
                      fontFamily: 'Vazir',
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                ),
                const SizedBox(height: 30),
                Text(
                  bmi,
                  style: const TextStyle(
                    fontSize: 60,
                    color: Colors.white,
                  ),
                ),
                const SizedBox(height: 20),
                Text(
                  name,
                  style: const TextStyle(
                    fontSize: 40,
                    color: Colors.white,
                  ),
                ),
                const SizedBox(height: 30),
                Slider(
                  min: 0,
                  max: 100,
                  value: slidernum,
                  onChanged: null,
                ),
                const SizedBox(height: 10),
                Row(
                  children: <Widget>[
                    const SizedBox(width: 30),
                    Container(
                      height: 20,
                      width: 60,
                      color: Colors.grey,
                    ),
                    Container(
                      height: 20,
                      width: 23,
                      color: Colors.green,
                    ),
                    Container(
                      height: 20,
                      width: 20,
                      color: Colors.yellow,
                    ),
                    Container(
                      height: 20,
                      width: 25,
                      color: const Color.fromARGB(255, 232, 112, 103),
                    ),
                    Container(
                      height: 20,
                      width: 200,
                      color: const Color.fromARGB(255, 238, 25, 10),
                    ),
                  ],
                ),
                const SizedBox(height: 30),
                helptext(),
              ],
            ),
          ),
        ),
      ),
    );
  }

  Widget helptext() {
    if (slidernum <= 18) {
      return ElevatedButton(
        style: ElevatedButton.styleFrom(
          backgroundColor: Colors.amber,
        ),
        onPressed: () {
          showDialog(
            context: context,
            builder: (BuildContext context) {
              return AlertDialog(
                backgroundColor: Colors.grey,
                elevation: 20,
                shape: const RoundedRectangleBorder(
                  borderRadius: BorderRadius.all(Radius.circular(20)),
                ),
                title: const Text(
                  'کمبود وزن دارید!!!',
                  textDirection: TextDirection.rtl,
                  textAlign: TextAlign.justify,
                  style: TextStyle(
                    fontSize: 30,
                    color: Color.fromARGB(255, 186, 74, 68),
                    fontWeight: FontWeight.bold,
                    fontFamily: 'Vazir',
                  ),
                ),
                content: const Text(
                  'س برای افزایش وزن بهتر است از این غذاها استفاده کنید. انتخاب های خوب شامل آب میوه 100 درصد طبیعی، شیر های کم چرب یا جایگزین های شیر ( مانند شیر سویا، شیر نارگیل و غیره ) و اسموتی هستند. اسموتی را می توانید با انواع خوراکی های خوب مثل جوانه گندم، کره بادام زمینی، آب هویج و عسل تقویت کنید.',
                  textDirection: TextDirection.rtl,
                  textAlign: TextAlign.justify,
                  style: TextStyle(
                    fontWeight: FontWeight.bold,
                    color: Colors.black,
                  ),
                ),
                actions: [
                  TextButton(
                    onPressed: () {},
                    style: TextButton.styleFrom(
                      foregroundColor: const Color.fromARGB(255, 186, 74, 68),
                    ),
                    child: const Text(
                      'متوجه شدم',
                      style: TextStyle(
                        fontSize: 20,
                        color: Color.fromARGB(255, 186, 74, 68),
                        fontFamily: 'Vazir',
                        fontWeight: FontWeight.w900,
                      ),
                    ),
                  ),
                ],
              );
            },
          );
        },
        child: const Text(
          '    پیشنهاد    ',
          style: TextStyle(
            fontSize: 30,
            color: Colors.black,
            fontWeight: FontWeight.w900,
          ),
        ),
      );
    } else if (slidernum >= 26) {
      return ElevatedButton(
        style: ElevatedButton.styleFrom(
          backgroundColor: Colors.amber,
        ),
        onPressed: () {
          showDialog(
            context: context,
            builder: (BuildContext context) {
              return AlertDialog(
                backgroundColor: Colors.grey,
                title: const Text(
                  'اضافه وزن دارید!!!',
                  textDirection: TextDirection.rtl,
                  textAlign: TextAlign.justify,
                  style: TextStyle(
                    fontSize: 30,
                    color: Color.fromARGB(255, 186, 74, 68),
                    fontWeight: FontWeight.bold,
                    fontFamily: 'Vazir',
                  ),
                ),
                content: const Text(
                  'برای کاهش‌وزن و حفظ آن باید از یک رژیم غذایی متعادل و مغذی پیروی کنید. این رژیم باید شامل همه‌ی گروه‌های غذایی از جمله نان و غلات، پروتئین‌ها، چربی‌ها و میوه‌ها و سبزیجات باشد. برای اثربخشی هرچه بیشتر به روند کاهش وزن می‌توانید برنامه ورزش یا پیاده روی را نیز در نظر داشته باشید.',
                  textDirection: TextDirection.rtl,
                  textAlign: TextAlign.justify,
                  style: TextStyle(
                    fontWeight: FontWeight.bold,
                    color: Colors.black,
                  ),
                ),
                actions: [
                  TextButton(
                    onPressed: () {},
                    style: TextButton.styleFrom(
                      foregroundColor: const Color.fromARGB(255, 186, 74, 68),
                      textStyle:
                          const TextStyle(fontFamily: 'Vazir', fontSize: 20),
                    ),
                    child: const Text(
                      'متوجه شدم',
                      style: TextStyle(
                        fontSize: 15,
                        color: Color.fromARGB(255, 186, 74, 68),
                        fontWeight: FontWeight.w900,
                      ),
                    ),
                  )
                ],
              );
            },
          );
        },
        child: const Text(
          '    پیشنهاد    ',
          style: TextStyle(
            fontSize: 30,
            color: Colors.black,
            fontWeight: FontWeight.w900,
          ),
        ),
      );
    }
    return Container();
  }

  Widget textflid2() {
    if (group == 1) {
      return TextFormField(
        autovalidateMode: AutovalidateMode.always,
        controller: _controller,
        keyboardType: TextInputType.number,
        decoration: const InputDecoration(
          hintText: 'قد(cm)',
          hintTextDirection: TextDirection.rtl,
          helperText: ' قد به سانتی متر',
          floatingLabelAlignment: FloatingLabelAlignment.start,
          helperStyle: TextStyle(
            color: Colors.white,
          ),
          disabledBorder: InputBorder.none,
          enabledBorder: InputBorder.none,
          hintStyle: TextStyle(
            fontFamily: 'Vazir',
            color: Colors.white,
            fontSize: 30,
            fontWeight: FontWeight.w300,
          ),
        ),
        textDirection: TextDirection.rtl,
        style: const TextStyle(
          color: Colors.yellow,
          fontSize: 40,
          fontWeight: FontWeight.w300,
        ),
        validator: (String? value) {
          if (value!.isEmpty) {
            return 'این فیلد را باید پر کنید';
          }
          if (group == 2 && value.length != 3) {
            return 'قد را درست وارد کنید';
          }
          if (double.parse(_controller.text) >= 220) {
            _controller.text = '';
          }
        },
      );
    }
    if (group == 2) {
      return TextFormField(
        autovalidateMode: AutovalidateMode.always,
        controller: _controller,
        keyboardType: TextInputType.number,
        decoration: const InputDecoration(
          hintText: 'قد(inch)',
          hintTextDirection: TextDirection.rtl,
          helperText: 'قد به اینچ',
          floatingLabelAlignment: FloatingLabelAlignment.start,
          helperStyle: TextStyle(
            color: Colors.white,
          ),
          disabledBorder: InputBorder.none,
          enabledBorder: InputBorder.none,
          hintStyle: TextStyle(
            fontFamily: 'Vazir',
            color: Colors.white,
            fontSize: 30,
            fontWeight: FontWeight.w300,
          ),
        ),
        textDirection: TextDirection.rtl,
        style: const TextStyle(
          color: Colors.yellow,
          fontSize: 40,
          fontWeight: FontWeight.w300,
        ),
        validator: (String? value) {
          if (value!.isEmpty) {
            return 'این فیلد را باید پر کنید';
          }
          if (group == 2 && value.length != 2) {
            return 'قد را درست وارد کنید';
          }
          if (double.parse(_controller.text) >= 150) {
            _controller.text = '';
          }
        },
      );
    }
    return const SizedBox();
  }
}

Color sliderColor(num value) {
  if (value < 18) {
    return Colors.grey;
  } else if (value < 25 && value >= 18) {
    return Colors.green;
  } else if (value < 29.9 && value >= 25) {
    return Colors.red;
  } else if (value < 34.9 && value >= 30) {
    return const Color.fromARGB(255, 72, 13, 9);
  }
  return Colors.black;
}
