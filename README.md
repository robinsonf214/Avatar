# Avatar
// Copyright (c) 2019, the Dart project authors.  Please see the AUTHORS file
// for details. All rights reserved. Use of this source code is governed by a
// BSD-style license that can be found in the LICENSE file.
import 'package:flutter/material.dart';
import 'dart:async';
import 'dart:math';
void main() => runApp(MyApp());
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const MyHomePage(title: 'Mario Bross'),
    );
  }
}
class MyHomePage extends StatefulWidget {
  final String title;
  const MyHomePage({
    Key? key,
    required this.title,
  }) : super(key: key);
  @override
  State<MyHomePage> createState() => _MyHomePageState();
}
class _MyHomePageState extends State<MyHomePage> {
  static double mariox = 0.0;
  static double marioy = 1.0;
  double time = 0;
  double height = 0;
  double initialPos = marioy;
  String direction = "right";
  void preJump() {
    time = 0;
    initialPos = marioy;
  }
  void jump() {
    preJump();
    Timer.periodic(Duration(milliseconds: 50), (timer) {
      time += 0.05;
      height = -4.9 * time * time + 5 * time;
      if (initialPos - height > 1) {
        setState(() {
          marioy = 1;
        });
      } else {
        setState(() {
          marioy = initialPos - height;
        });
      }
    });
  }
  void walkL() {
    direction = "left";
    setState(() {
      mariox -= 0.02;
    });
  }
  void walkR() {
    direction = "right";
    setState(() {
      mariox += 0.02;
    });
  }
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Column(children: [
        
         Container(
         color: Colors.blue,
         child: Row(mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                children:const<Widget>[
                 Text('Vida:', style: TextStyle(color: Colors.white,fontSize: 20),),
                 Text('Puntos:', style: TextStyle(color: Colors.white,fontSize: 20),),
                 Text('Tiempo:', style: TextStyle(color: Colors.white,fontSize: 20),)
                  ])
           ),
        Expanded(
            flex: 4,
            child: Container(
                color: Colors.blue,
                child: AnimatedContainer(
                    alignment: Alignment(mariox, marioy),
                    duration: Duration(milliseconds: 0),
                    child: Mario(
                      direction: direction,)
                    )
                )
            
            ),
        Expanded(
            flex: 4,
            child: Container(
                color: Colors.blue,
                child: AnimatedContainer(
                    alignment: Alignment(mariox, marioy),
                    duration: Duration(milliseconds: 0),
                    child: Robin(
                      direction: direction,)
                    )
                )
            
            ),
        Container(height: 10, color: Colors.green),
        Expanded(
            flex: 1,
            child: Container(
                color: Colors.brown,
                child: Row(
                    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                    children: [
                      GestureDetector(
                          onTap: walkL,
                          child: Container(
                            padding: EdgeInsets.all(10),
                            color: Colors.brown[300],
                            child: Icon(Icons.arrow_back),
                          )),
                      GestureDetector(
                          onTap: jump,
                          child: Container(
                            padding: EdgeInsets.all(10),
                            color: Colors.brown[300],
                            child: Icon(Icons.arrow_upward),
                          )),
                      GestureDetector(
                          onTap: walkR,
                          child: Container(
                              padding: EdgeInsets.all(10),
                              color: Colors.brown[300],
                              child: Icon(Icons.arrow_forward))),
                    ])))
      ]),
    );
  }
}
class Mario extends StatelessWidget{
  
  final direction;
  
  Mario({this.direction});
  
  @override
  Widget build(BuildContext context){
    if (direction == "right"){
      return Container(
        width: 50,
        height: 50,
        child: Image.network(
                        "https://cdn.pixabay.com/photo/2021/02/11/15/40/mario-6005703_960_720.png")
      );
    }else{
      return Transform(
        alignment: Alignment.center,
        transform: Matrix4.rotationY(pi),
        child: Container(
        width: 50,
        height: 50,
        child: Image.network(
                        "https://cdn.pixabay.com/photo/2021/02/11/15/40/mario-6005703_960_720.png")
      ));
    }
  }
  
}

class Robin extends StatelessWidget{
  
  final direction;
  
  Robin({this.direction});
  
  @override
  Widget build(BuildContext context){
    if (direction == "left"){
      return Container(
        width: 50,
        height: 50,
        child: Image.network(
                        "https://raw.githubusercontent.com/robinsonf214/Avatar/main/avatar.png")
      );
    }else{
      return Transform(
        alignment: Alignment.center,
        transform: Matrix4.rotationY(pi),
        child: Container(
        width: 50,
        height: 50,
        child: Image.network(
                        "https://raw.githubusercontent.com/robinsonf214/Avatar/main/avatar.png")
      ));
    }
  }
  
}
