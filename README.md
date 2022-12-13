# apb_protocol_with_decoder
apb protocol 
It is a protocol which guides the selections and data flow from peripherals to an SoC , it works at lower frequency than AHB and it is based on AMBA,
the frequency of working is around 100Mhz i.e 10ns period clock.
In apb protocol there will be a decoder which will decode the address to select the slave i.e Pselx signal is assigned based on the address range.
According to protocol spec sheet it has 3 states in it's state machine they are:
   1.IDLE state or reset state
   2.SETUP state the psel decoding state.
   3.ACCESS state the operation state.
signals:
   1.psel - this tells which slave is working.
   2.penable - this will enable the transaction.
   3.pready - this signal will decide whether to change from the access state(generally asserted once the operation is completed from slave's end).
with wait states and without wait states:
   1. without wait states : your pready can be kept always high or should be high in access state i.e for one cycle.
      in this generally the completion of transaction occurs in maximum of 3 clock cycles.
   2. with wait states : your pready can be asserted high before setup clock edge and to make wait pready should be driven low till the delay then make 
      it high when the delay is over.
whenever the operation starts psel will be asserted high, then after one clock penable will be asserted high, then right with that edge pready will be high
or operation ends if no wait state, if there is wait state then pready will made zero to make the wait states the will be asserted high once the delay over.
above is for decoder
slave: in slave the write operation will be sequential and read operation will be combinational.
the code here is kind of not fully apb multi slave tested, i've tried for one slave and have done state machine for multiple slave but yet to write 
random data an random address with pslverr in this code. 
"any kind of corrections let me know"
contact : mahanthadeekshasb@gmail.com

