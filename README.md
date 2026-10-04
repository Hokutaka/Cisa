# Cisa

自作言語でCPUを作ってみたくなった。  
なんだかよく分からないけど、Ceruneに `emit-fpga` を作っても面白いかもしれないという話がある（ほんとうか？）  
ただ、いきなりFPGAに行ってもなにが必要なのか分からないので、まずはCeruneで仮想CPUを泥臭く実装してみることにした。  
そのためにCPU、命令セット、メモリ、スタック、I/Oあたりを実際に作っていくことで、DogfoodingでCeruneにはなにが足りないのかを確認できるはず、という考え方をしています。  

## やりたいこと

最終的には、Cerune上で小さなコンピュータを一通り作ってみたいです。

```text
Cisa
├─ CPU
│  ├─ Registers
│  ├─ Program Counter
│  ├─ ALU
│  ├─ Flags
│  └─ Instruction Decoder
│
├─ ISA
│  ├─ Arithmetic
│  ├─ Bit operations
│  ├─ Branch
│  ├─ Load / Store
│  ├─ Call / Return
│  └─ I/O
│
├─ Memory
│  ├─ ROM
│  ├─ RAM
│  └─ Stack
│
├─ Devices
│  ├─ Timer
│  ├─ Controller Input
│  ├─ Framebuffer
│  └─ Sound?
│
├─ Tooling
│  ├─ Assembler
│  ├─ Debug / Trace
│  └─ ROM image
│
└─ Software
   ├─ Boot ROM
   ├─ Runtime / small OS?
   └─ Games / Programs
```

まずは32bit程度の小さな仮想CPUとして作っていく予定です。  
CPUだけで終わらず、RAM、スタック、割り込み、タイマー、画面、入力なども実装して、最終的には小さな仮想ゲーム機くらいまで持っていけたら面白そうです。  
その過程でCerune側に必要になった機能は、実際の用途を見ながら追加していきます。  
そして、もし本当にCeruneからハードウェアを生成できそうなら、  

```text
Cisa
  ↓
Cerune
  ↓
FPGA向けの何か
  ↓
Verilog?
  ↓
FPGA
```

みたいなところまで行ってみたいです。  
今のところ、そこまで本当に行けるのかは分かりません。  
その確認も含めてCisaを作ります。  

# 名前の由来

Cerune ISA から Cisa。