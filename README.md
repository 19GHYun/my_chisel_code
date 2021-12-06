# my_chisel_code


import chisel3._
import chisel3.util.Enum



class GradLife extends Module {
  val io = IO(new Bundle {
    val state = Input(UInt(2.W))
    val F = Input(Bool())
    val H = Input(Bool())
    //val pressure = Input(Bool())
    val nextState = Output(UInt(2.W))
    val y = Output(UInt(1.W))
  })
  val idle :: fifty :: hundred :: hf :: Nil = Enum(4)

  io.nextState := idle
  when (io.state === idle) {
    when      (io.F) { io.nextState := fifty }
      .elsewhen (io.H) { io.nextState := hundred }
      //.elsewhen (io.pressure) { io.nextState := writing }
  } .elsewhen (io.state === fifty) {
    when      (io.F) { io.nextState := hundred }
      .elsewhen (io.H) { io.nextState := hf }
  } .elsewhen (io.state === hundred) {
    when      (io.F || io.H) { io.nextState := hf }
      //.elsewhen (io.pressure) { io.nextState := grad }
  } .elsewhen (io.state === hf){
    io.y == 1
    io.nextState === idle
  }

}


![1111](https://user-images.githubusercontent.com/94778099/144800694-7b3f84ae-65ac-4d0d-bb30-7284c976e065.png)


[20194546_Vending_Mechine_.xlsx](https://github.com/19GHYun/my_chisel_code/files/7658584/20194546_Vending_Mechine_.xlsx)
