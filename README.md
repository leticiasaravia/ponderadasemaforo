# 🚦 Projeto: Semáforo para o Butantã (com POO e Ponteiros)

## Objetivo

Implementar um **sistema de semáforo** utilizando **C++ no Arduino**, aplicando os conceitos de **Programação Orientada a Objetos (POO)** e **uso de ponteiros**.  
O projeto visa demonstrar a criação de uma classe para representar LEDs, permitindo um controle modular e reutilizável do sistema de sinalização luminosa.

## ⚙️ Componentes Utilizados

| Componente | Quantidade | Pino no Arduino |
|-------------|-------------|-----------------|
| LED Vermelho | 1 | **10** |
| LED Amarelo | 1 | **11** |
| LED Verde | 1 | **12** |
| Resistores | 3 |
| Protoboard | 1 | — |
| Jumpers | 8 | — |


## 💻 Código-Fonte

```cpp
// CLASSE LED 
class Led {
  private:
    int* pino; // Ponteiro para o número do pino

  public:
    // Construtor: inicializa o pino do LED
    Led(int* p) {
      pino = p;
      pinMode(*pino, OUTPUT);
    }

    // Liga o LED
    void ligar() {
      digitalWrite(*pino, HIGH);
    }

    // Desliga o LED
    void desligar() {
      digitalWrite(*pino, LOW);
    }
};

// ---------- VARIÁVEIS GLOBAIS ----------
int pinoVermelho = 10;  // 🔴 LED Vermelho
int pinoVerde = 12;     // 🟢 LED Verde
int pinoAmarelo = 11;   // 🟡 LED Amarelo

// Ponteiros para os objetos LED
Led* ledVermelho;
Led* ledVerde;
Led* ledAmarelo;

// ---------- CONFIGURAÇÃO INICIAL ----------
void setup() {
  // Criação dinâmica dos objetos LED
  ledVermelho = new Led(&pinoVermelho);
  ledVerde = new Led(&pinoVerde);
  ledAmarelo = new Led(&pinoAmarelo);
}

// ---------- LOOP PRINCIPAL ----------
void loop() {
  // Fase 1 - Vermelho (6 segundos)
  ledVermelho->ligar();
  ledVerde->desligar();
  ledAmarelo->desligar();
  delay(6000);

  // Fase 2 - Verde (4 segundos)
  ledVermelho->desligar();
  ledVerde->ligar();
  ledAmarelo->desligar();
  delay(4000);

  // Fase 3 - Amarelo (2 segundos)
  ledVerde->desligar();
  ledAmarelo->ligar();
  ledVermelho->desligar();
  delay(2000);
}
```

## Estrutura Orientada a Objetos

| Conceito | Aplicação no Código |
|-----------|--------------------|
| **Classe (`Led`)** | Representa um LED com seus métodos e atributo de pino. |
| **Encapsulamento** | O pino é privado, acessado apenas pelos métodos da classe. |
| **Ponteiros** | Cada LED é criado dinamicamente com `new`, usando ponteiro para o pino (`int*`). |
| **Abstração** | O controle de cada LED é feito por métodos simples (`ligar()` e `desligar()`). |


## Funcionamento do Semáforo

| Fase | LED Ativo | Duração | Ação |
|------|------------|----------|------|
| 1 | 🔴 Vermelho | 6s | Interrompe o tráfego. |
| 2 | 🟢 Verde | 4s | Libera o tráfego. |
| 3 | 🟡 Amarelo | 2s | Alerta para mudança. |

## Lógica de Execução

1. O programa inicializa os LEDs por meio de **objetos criados dinamicamente**.  
2. No `loop()`, o semáforo alterna as cores em um **ciclo contínuo**.  
3. Cada transição respeita o tempo configurado em `delay()`.  
4. Os ponteiros permitem gerenciar os LEDs sem instâncias fixas na memória.


## Benefícios do Uso de POO e Ponteiros

- **Reutilização de código:** a classe `Led` pode ser aplicada em outros projetos.  
- **Facilidade de manutenção:** cada LED é independente.  
- **Eficiência:** ponteiros reduzem o uso desnecessário de memória estática.  
- **Modularidade:** separa o controle lógico (POO) da camada física (hardware).  


## Tutorial de Montagem — Passo a Passo

###  Visão geral do circuito


###  Passo 1 — Conexão dos LEDs
1. Insira os **três LEDs** (vermelho, amarelo e verde) na protoboard, em linhas separadas.  
2. Conecte o **catodo (perna menor)** de cada LED ao **GND** do Arduino.  
3. Conecte o **ânodo (perna maior)** de cada LED a um **resistor de 220 Ω**.  


### Passo 2 — Conexão dos resistores aos pinos digitais
Ligue a outra extremidade dos resistores aos pinos digitais do Arduino:

- 🔴 **Vermelho → pino 10**  
- 🟡 **Amarelo → pino 11**  
- 🟢 **Verde → pino 12**


### Passo 3 — Conexão de energia
- Conecte o **GND** da protoboard ao **GND** do Arduino.  
- Conecte o **Arduino ao computador** via cabo USB.


### Passo 4 — Upload do código
1. Abra a **IDE do Arduino**.  
2. Cole o código do semáforo (arquivo sugerido: `src/semaforo.ino`).  
3. Selecione a **placa** (ex.: Arduino Uno) e a **porta** correta.  
4. Clique em **Upload**.  
5. Observe os LEDs alternando conforme as fases do semáforo (6s vermelho, 4s verde, 2s amarelo).


### Demonstração em Vídeo
**Link do vídeo:** 

## Conclusão

Conclusão

O desenvolvimento deste projeto permitiu aplicar de forma prática os conceitos fundamentais de **Programação Orientada a Objetos (POO)** e **manipulação de ponteiros em C++**, integrando-os ao controle físico de hardware com o **Arduino**.  

A criação da classe `Led` demonstrou como a abstração e o encapsulamento tornam o código mais organizado, facilitando futuras expansões, como a inclusão de sensores ou comunicação entre semáforos.  
Além do aspecto técnico, o projeto evidencia a importância da **integração entre software e eletrônica** na construção de soluções inteligentes para o trânsito urbano, contribuindo para a segurança e fluidez viária.  

Assim, o sistema desenvolvido alcança todos os objetivos propostos — unindo **precisão lógica, estrutura modular e execução fiel às temporizações reais de um semáforo**.

## Critérios Atendidos

Estrutura POO com classe e encapsulamento  
Uso de ponteiros para acesso aos pinos  
Ciclo completo de semáforo (vermelho → verde → amarelo)  
Temporização correta  
Documentação completa 
Código funcional
