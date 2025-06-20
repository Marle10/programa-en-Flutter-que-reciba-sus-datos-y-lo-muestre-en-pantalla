# programa-en-Flutter-que-reciba-sus-datos-y-lo-muestre-en-pantalla

import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) => const MaterialApp(
        home: FormularioScreen(),
        debugShowCheckedModeBanner: false,
      );
}

class FormularioScreen extends StatefulWidget {
  const FormularioScreen({super.key});

  @override
  State<FormularioScreen> createState() => _FormularioScreenState();
}

class _FormularioScreenState extends State<FormularioScreen> {
  final nombreCtrl = TextEditingController();
  final edadCtrl = TextEditingController();
  final matriculaCtrl = TextEditingController();
  final correoCtrl = TextEditingController();
  String resultado = '';

  void mostrarDatos() {
    setState(() {
      resultado =
          'Nombre: ${nombreCtrl.text}\nEdad: ${edadCtrl.text}\nMatrícula: ${matriculaCtrl.text}\nCorreo: ${correoCtrl.text}';
    });
  }

  Widget campo(String label, TextEditingController controller,
      {TextInputType tipo = TextInputType.text}) {
    return Padding(
      padding: const EdgeInsets.symmetric(vertical: 8),
      child: TextField(
        controller: controller,
        keyboardType: tipo,
        decoration: InputDecoration(
          labelText: label,
          border: OutlineInputBorder(borderRadius: BorderRadius.circular(12)),
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) => Scaffold(
        appBar: AppBar(title: const Text('Formulario de Datos')),
        body: SingleChildScrollView(
          padding: const EdgeInsets.all(16),
          child: Column(
            children: [
              campo('Nombre', nombreCtrl),
              campo('Edad', edadCtrl, tipo: TextInputType.number),
              campo('Matrícula', matriculaCtrl),
              campo('Correo', correoCtrl, tipo: TextInputType.emailAddress),
              const SizedBox(height: 16),
              ElevatedButton(
                onPressed: mostrarDatos,
                child: const Text('Mostrar Datos'),
              ),
              const SizedBox(height: 20),
              Text(
                resultado,
                style: const TextStyle(fontSize: 18),
                textAlign: TextAlign.center,
              )
            ],
          ),
        ),
      );
}
