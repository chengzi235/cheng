中断
=========

中断的两种方式
--------------

- 传统方式(INTx)
    - PCI 系统中

    在最早的PCI总线系统中，每个设备的中断是通过实际的硬件连线连接到CPU
    的中断控制器上，现在基本不使用了，可以忽略。

    .. figure:: _images/legacy_interrupt_example.png
        :align: center
        :target: _images/legacy_interrupt_example.png

        *Legacy Interrupt Example*

    - PCIe 系统中

    在后来的PCIe系统中为了兼容传统的PCI设备会通过Message来对传统的中断进行模拟。

    .. figure:: _images/interrupt_delivery_options_in_PCIe_sytem.png
        :align: center
        :target: _images/interrupt_delivery_options_in_PCIe_sytem.png

        *Interrupt Delivery Options in PCIe System*

    - Interrupt Registers

    在PCI配置空间里面与INTx相关的寄存器。

    .. figure:: _images/interrupt_registers_in_PCI_configuration_header.png
        :align: center
        :target: _images/interrupt_registers_in_PCI_configuration_header.png

        *Interrupt Registers in PCI Configuration Header*

    .. figure:: _images/configuration_command_register-interrupt_disable_field.png
        :align: center
        :target: _images/configuration_command_register-interrupt_disable_field.png

        *Configuration Command Register — Interrupt Disable Field*

    Interrupt disable bit在复位时会被清除从而允许设备产生INTx中断，但是软件可以置位
    该bit来阻止设备产生中断。需要注意的是，该bit对MSI中断没有影响，MSI中断
    通过 MSI Capability structure 中的 Command Register 来使能或者禁用，然而，当使能
    MSI中断时INTx中断会被自动禁用。
    
    .. figure:: _images/configuration_status_register—interrupt_status_field.png
        :align: center
        :target: _images/configuration_status_register—interrupt_status_field.png

        *Configuration Status Register — Interrupt Status Field*

    Interrupt status bit置位时说明有中断发生。需要注意，当桥在转发下游设备模拟INTx
    中断的消息时不会对该位造成影响。

    - PCIe系统中对INTx的模拟

    .. figure:: _images/example_of_INTx_messages_to_virtualize_INTA‐INTD.png
        :align: center
        :target: _images/example_of_INTx_messages_to_virtualize_INTA‐INTD.png

        *Example of INTx Messages to Virtualize INTA#‐INTD# Signal Transitions*

    .. figure:: _images/INTx_message_format_and_type.png
        :align: center
        :target: _images/INTx_message_format_and_type.png

        *INTx Message Format and Type*


- 基于消息的方式


  - MSI

  - MSI-X
