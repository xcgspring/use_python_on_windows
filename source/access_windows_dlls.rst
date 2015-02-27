.._'User Python to access windows DLL or COM interface:
1 call convention
   The conventional types incluede the following,usually used cdecl or stdcall: 
   cdecl: The abbreviation of C Decalaration,C/C++ calls by default.
   stdcall:The abbreviation of StandardCall,C++ standard call way.
   fastcall:
   thiscall:
   nakedcall:
   
2 ctypes
    Ctypes by encapsulating 'dlopen/dlsym' functions like, and to provide to pack/unpack data structure in C, 
	allow Python to load dynamic libraries, export directly use the function of them. 
    (1) ctypes's data type
	    ctypes and  c corresponding data types are listed in the table below
		+===========+==========+
		|  C        |  ctypes  |
		+===========+==========+
		|char	    | c_char   |                      
        |short	    | c_short  | 
        |int 	    | c_int    |                          
        |long 	    | c_long   |                        
        |unsign long| c_ulong  |                      
        |float 	    | c_float  |                        
        |double     | c_double |                     
        |void 	    | c_void_p |
		+===========+==========+
	                   

	(2) import model
	     from ctypes import*
		 
	(3) load DLL
	      cdelc
		    Objdll = ctypes.cdll.LoadLibrary("dllpath")  
            Objdll = ctypes.CDLL("dllpath")  

		  stdcall
		    Objdll = ctypes.windll.LoadLibrary("dllpath")  
            Objdll = ctypes.WinDLL("dllpath")  

	(4) call the methode from DLL
	      Ordinary type parameter
		      value = dll.Add(1, 102) 
		      print value
			  
		  Point type parameter 
		     The point type parameter can used the byref:
			  intPara = c_int(9)  
              dll.sub(23, 102, byref(intPara))  

		   
	(5) return value
	       if return value is point , must conversion it to corresponding python data type.
		      pchar = dll.getbuffer()  
              szbuffer = c_char_p(pchar)  
              print szbuffer.value  

	(6) the structure of C
	
	(7) eg:
	    -----C++---------------
	    /hello.h
        #ifdef EXPORT_HELLO_DLL
        #define HELLO_API __declspec(dllexport)
        #else
        #define HELLO_API __declspec(dllimport)
        #endif
        extern "C"
        {
          HELLO_API int IntAdd(int , int);
         }
	
	    //hello.cpp
        define EXPORT_HELLO_DLL
        #include "hello.h"
        HELLO_API int IntAdd(int a, int b)
        {
          return a + b;
        }
  
        -----python------------
        from ctypes import *
        dll = cdll.LoadLibrary('hello.dll');
        ret = dll.IntAdd(2, 4);
        print ret;
	 
3 comtypes
4 win32 DLL
    (1) install pywin32.exe
	    The first your must install pywin32.exe.
		
	(2) import module
	     you need to import the follwing several modules:
		   import win32api,win32gui
		   import win32con,winerrir,pywintyoes
	(3) eg
	     eg:
          import win32api, win32gui
          import win32con, winerror,win32event,pywintypes
          from ctypes import *

          def main():
          win32api.MessageBox(0, 'Hello,Win32API', 'WYM', win32con.MB_OK)