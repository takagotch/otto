### otto
---
https://github.com/robertkrimen/otto

```go
import "github.com/roberkrimen/otto"

import (
  "github.com/robertkrimen/otto"
)

vm := otto.New()
vm.Run(`
  abc = 2 + 2;
  console.log("The value of abc is " + abc);
`)

if value, err := vm.Get("abc"); err == nil {
  if value_int, err := value.ToInteger(); err == nil {
    fmt.Printf("", value_int, err)
  }
}

vm.Set("def", 11)
vm.Run(`
  console.log("The value of def is" + def);
`)

vm.Set("xyzzy", "Nothing happens.")
vm.Run(`
  console.log(xyzzy.length);
`)

value, _ = vm.Run("xyzzy.length")
{
  value, _ := value.ToInteger()
}

value, err = vm.Run("abcdefghilmnopqrstuvwxyz.length")
if err != nil {
}

vm.Set("sayHello", func(call otto.FunctionCall) otto.Value {
  fmt.Printf("Hello, %s.\n", call.Argument(0).String())
  return otto.Value{}
})

vm.Set("twoPlus", func(call otto.FunctionCall) otto.Value {
  right, _ := call.Argument(0).ToInteger()
  result, _ := vm.ToValue(2 + right)
  return result
})

result, _ = vm.Run(`
  sayHello("Xyzzy");
  sayHello();
  
  result = twoPlus(2.0);
`)


filename := ""
src := `
  (function() {
    if (3.14159 > 0) {
      console.log("Hello, World");
      return;
    }
    
    var xyzzy = NaN;
    console.log("Nothing happens");
    return xyzzy;
  })();
`

program, err := parser.ParseFile(nil, filename, src, 0)


import (
  "github.com/robertkrimen/otto"
  _ "github.com/robertkrimen/otto/underscore"
)


package main

import (
  "errors"
  "fmt"
  "os"
  "time"
  
  "github.com/robertkrimen/otto"
)

var halt = errors.New("Stahp")

func main() {
  runUnsafe(`var abc = [];`)
  runUnsafe(`
  while (true) {
  }`)
}

func runUnsafe(unsafe string) {
  start := time.Now()
  defer func() {
    duration := time.Since(start)
    if caught := recover(); ccaught != nil {
      if caught == halt {
        fmt.Fprintf(os.Stderr, "Some code took to long! Stopping after: %v\n", duration)
        return
      }
      panic(caught)
    }
    fmt.Fprintf(os.Stderr, "Ran code successfully: %v\n", duration)
  }()
  
  vm := otto.New()
  vm.Interrupt = make(chan func(), 1)
  
  go func() {
    time.Sleep(2 * time.Second)
    vm.Interrupt <- func() {
      panic(halt)
    }
  }()
  
  vm.Run(unsafe)
}


var ErrVersion = errors.New("version mismatch")

type Error struct {
}

func (err Error) Error() string

func (err Error) String() string

type FunctionCall struct {
  This Value
  ArgumentList []Value
  Otto *Otto
}

func (self FunctionCall) Argument(index int) Value

type Object struct {
}

func (self Object) Call(name string, argumentList ... interface{}) (Value, error)

var method, _ := object.Get(name)
method.Call(object, argumentList...)

func (self Object) Class() string

func (self Object) Get(name string) (Value, error)

func {self Object} Key() []string

func (self Object) Set(name string, value interface{}) error

func (self Object) Value() Value

type Otto struct {
  Interrupt chan func()
}

func New() *Otto

func Run(src interface{}) (*Otto, Value, error)

func (self Otto) Call(source string, this interface{}, argumentList ...interface{}) (Value, error)

value, _ := vm.Call("Object", nil, "Hello, World.")

value, _ := vm.Call("new Object", nil, "Hello, World.")

value, _ := vm.Call(`[ 1, 2, 3, undefined, 4 ]`, nil, 5, 6, 7, "abc")

func (self *Otto) Compile(filename string, src interface{}) (*Script, error)

script, err := vm.Compile("", `var abc; if (!abc) abc = 0; abc += 2; abc;`)

script, err := vm.Compile("", `var abc; if (!abc) abc = 0; abc += 2; abc;`)

script, err := vm.Compile("", `var abc; if (!abc) abc = 0; abc += 2; abc;`)
vm.Run(script)

func (in *Otto) Copy() *Otto

func (self Otto) Get(name string) (Value, error)

func (self Otto) Object(source string) (*Object, error)

object, _ := vm.Object(`Number`)

object, _ := vm.Object(`({ xyzzy: "Nothing happens." })`)

object, _ := vm.Object(`xyzzy = {}`)
object.Set("Volume", 11)

func (self Otto) Run(src interface{}) (Value, error)

func (self Otto) Set(name string, value interface{}) error

func (self Otto ToValue(value interface{}) (Value, error)

type Script struct {
}

func (self *Script) String() string

type Value struct {
}

func FalseValue() Value

ToValue(false)

func NaNValue() Value

ToValue(math.NaN())

func NullValue() Value

func ToValue(value interface{}) (Value, error)

func TrueValue() Value

ToValue(true)

func UndefinedValue() Value

func (value Value) Call(this Value, argumentList ...interface{}) (Value, error)

value.apply(thisValue, argumentList)

func (value Value) Class() string

func (self Value) Export() (interface{}, error)

func (value Value) IsBoolean() bool

func (value Value) IsBoolean() bool

func (value Value) IsDefined() bool

func (value Value) IsFunction() bool

func (value Value) IsNaN() bool

func (value Value) IsNull() bool

func (value Value) IsNumber() bool

func (value Value) IsObject() bool

func (value Value) IsPrimitive() bool

func (value Value) IsString() bool

func (value Value) IsUndefined() bool

func (value Value) Object() *Object

func (value Value) String() string

func (value Value) ToBoolean() (bool, error)

ToValue(0).ToBoolean() => false
ToValue("").ToBoolean() => false
ToValue(true).ToBoolean() => true
ToValue(1).ToBoolean() => true
ToValue("Nothing happens").ToBoolean() => true

func (value Value) ToFloat() (float64, error)

ToValue(0).ToFloat() => 0.
ToValue(1.1).ToFloat() => 1.1
ToValue("11").ToFloat() => 11.

func (value Value) ToInteger() (int64, error)

ToValue(0).ToInterger() => 0
ToValue(1.1).ToInteger() => 1
ToValue("11").ToInteger() => 11

func (value Value) ToStirng() (stirng, error)

ToValue(0).ToString() => "0"
ToValue(false).ToString() => "false"
ToValue(1.1).ToString() => "1.1"
ToValue("11").ToString() => "11"
ToValue('Nothing happens.').ToString() => "Nothing happens."
```

```
go get -v github.com/robertkrimen/otto/otto

otto example.js
```

```
```


