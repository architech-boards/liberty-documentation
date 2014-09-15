.. index:: linker

.. _lfile:

Linker file contents
********************

This is the contents of linker file named **Liberty_BLE_v1_HardwareDebug_auto.gsi**

::

 MEMORY
 {
	VEC : ORIGIN = 0x0, LENGTH = 4
	IVEC : ORIGIN = 0x4, LENGTH = 124
	SEC_ID : ORIGIN = 0xC4, LENGTH = 12
	OPT_BYTES : ORIGIN = 0xC0, LENGTH = 4
	ROM : ORIGIN = 0xD8, LENGTH = 65320
	RAM : ORIGIN = 0xFEF00, LENGTH = 3872
 }

 SECTIONS
 {
	.vec 0x0 : AT (0x0)
	{
		KEEP(*(.vec))
	} > VEC
	.vects 0x4 : AT (0x4)
	{
		KEEP(*(.vects))
	} > IVEC
	.option_bytes 0xC0 : AT (0xC0)
	{
		*(.option_bytes)
	} > OPT_BYTES
	.security_id 0xC4 : AT (0xC4)
	{
		*(.security_id)
	} > SEC_ID
	.secti_rom 0xD8 : AT (0xD8)
	{
	} > ROM
	.rodata 0x2000 : AT (0x2000)
	{
		. = ALIGN(2);
		*(.rodata)
		*(.rodata.*)
		_erodata = .;
	} > ROM
	.text : 
	{
		*(.text)
		*(.text.*)
		etext = .;
		. = ALIGN(2);
	} > ROM
	.init : 
	{
		*(.init)
	} > ROM
	.fini : 
	{
		*(.fini)
	} > ROM
	.got : 
	{
		*(.got)
		*(.got.plt)
	} > ROM
	.eh_frame_hdr : 
	{
		*(.eh_frame_hdr)
	} > ROM
	.eh_frame : 
	{
		*(.eh_frame)
	} > ROM
	.jcr : 
	{
		*(.jcr)
	} > ROM
	.tors : 
	{
		__CTOR_LIST__ = .;
		. = ALIGN(2);
		___ctors = .;
		*(.ctors)
		___ctors_end = .;
		__CTOR_END__ = .;
		__DTOR_LIST__ = .;
		___dtors = .;
		*(.dtors)
		___dtors_end = .;
		__DTOR_END__ = .;
		. = ALIGN(2);
		_mdata = .;
	} > ROM
	.data 0xFEF00 : AT (_mdata)
	{
		. = ALIGN(2);
		_data = .;
		*(.data)
		*(.data.*)
		. = ALIGN(2);
		_edata = .;
	} > RAM
	.bss : 
	{
		. = ALIGN(2);
		_bss = .;
		*(.bss)
		*(.bss.**)
		. = ALIGN(2);
		*(COMMON)
		. = ALIGN(2);
		_ebss = .;
		_end = .;
	} > RAM
	.stack 0xFFE00 (NOLOAD)  : AT (0xFFE00)
	{
		_stack = .;
	} > RAM
 }



