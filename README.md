# ian.game table of contents

## Types

+ [ian.game.Input](#lfcswacztut55eosrmx67k26ee)
+ [ian.game.Model](#h33hgxxlvdmsc7sdtoaegobq6y)
+ [ian.game.UI](#qnhffirgwclqtybjurdbunbcvy)

## Terms

+ [ian.game.UI.init](#i6xxztlawhulufmy6ofmmzaktq)
+ [ian.game.UI.init.modify](#7jrpenauytbdmvkyk7c5m7ef5i)
+ [ian.game.UI.init.set](#6nijsvqwvlvgw3bmj4hkb6yqaa)
+ [ian.game.UI.parseInput](#5gj55dwxgauyednupxac45zjna)
+ [ian.game.UI.parseInput.modify](#tma53awkw7clzfu2ojt4rfywcm)
+ [ian.game.UI.parseInput.set](#hx2j3zw6oo7qxglyvl2xv37pqm)
+ [ian.game.UI.update](#kzv6ncavoi64qddyezxrqvfmeu)
+ [ian.game.UI.update.modify](#jx5qziohooyhb4w6l4ef5s3nce)
+ [ian.game.UI.update.set](#gbw5xrj7dm6wwaaurpricwllne)
+ [ian.game.UI.view](#u5rv464dfi6ystqmujtfs4mpxm)
+ [ian.game.UI.view.modify](#3jm6dxygrldgsgnxj6pbm7pux4)
+ [ian.game.UI.view.set](#xtos26q5fgjx7otknj3i5lvxsa)
+ [ian.game.chips](#r5qojxh6x4tvyy7ldi37q7axya)
+ [ian.game.init](#onfcdmfwvmlwi46pv7dlxhebvu)
+ [ian.game.parseGameInput](#syltqd63agtx42qlokljtx6yqq)
+ [ian.game.playChip](#d42enpvm62uistugq37fhjn3ha)
+ [ian.game.run](#yds6zitmtv7aagdtbqunw7gbve)
+ [ian.game.update](#t7o7zhxnkh57vg6vu35l5xqdvm)
+ [ian.game.view](#ozy5egc54p3inmcov6kyuzkqji)

# Types

<a name='lfcswacztut55eosrmx67k26ee'/>

### ian.game.Input

```unison
unique type ian.game.Input = Input
```

<a name='h33hgxxlvdmsc7sdtoaegobq6y'/>

### ian.game.Model

```unison
unique type ian.game.Model = Model
```

<a name='qnhffirgwclqtybjurdbunbcvy'/>

### ian.game.UI

```unison
unique type ian.game.UI model input
  = { init : ian.game.Model,
      view : model -> builtin.Text,
      update : input -> model -> model,
      parseInput : builtin.Text -> builtin.Either builtin.Text input }
```


# Terms

<a name='i6xxztlawhulufmy6ofmmzaktq'/>

### ian.game.UI.init

```unison
ian.game.UI.init uI = case uI of ian.game.UI.UI init _ _ _ -> init
```

<a name='7jrpenauytbdmvkyk7c5m7ef5i'/>

### ian.game.UI.init.modify

```unison
ian.game.UI.init.modify f uI =
  use ian.game.UI UI
  case uI of
    UI init view update parseInput -> UI (f init) view update parseInput
```

<a name='6nijsvqwvlvgw3bmj4hkb6yqaa'/>

### ian.game.UI.init.set

```unison
ian.game.UI.init.set init1 uI =
  use ian.game.UI UI
  case uI of UI _ view update parseInput -> UI init1 view update parseInput
```

<a name='5gj55dwxgauyednupxac45zjna'/>

### ian.game.UI.parseInput

```unison
ian.game.UI.parseInput uI =
  case uI of ian.game.UI.UI _ _ _ parseInput -> parseInput
```

<a name='tma53awkw7clzfu2ojt4rfywcm'/>

### ian.game.UI.parseInput.modify

```unison
ian.game.UI.parseInput.modify f uI =
  use ian.game.UI UI
  case uI of
    UI init view update parseInput -> UI init view update (f parseInput)
```

<a name='hx2j3zw6oo7qxglyvl2xv37pqm'/>

### ian.game.UI.parseInput.set

```unison
ian.game.UI.parseInput.set parseInput1 uI =
  use ian.game.UI UI
  case uI of UI init view update _ -> UI init view update parseInput1
```

<a name='kzv6ncavoi64qddyezxrqvfmeu'/>

### ian.game.UI.update

```unison
ian.game.UI.update uI = case uI of ian.game.UI.UI _ _ update _ -> update
```

<a name='jx5qziohooyhb4w6l4ef5s3nce'/>

### ian.game.UI.update.modify

```unison
ian.game.UI.update.modify f uI =
  use ian.game.UI UI
  case uI of
    UI init view update parseInput -> UI init view (f update) parseInput
```

<a name='gbw5xrj7dm6wwaaurpricwllne'/>

### ian.game.UI.update.set

```unison
ian.game.UI.update.set update1 uI =
  use ian.game.UI UI
  case uI of UI init view _ parseInput -> UI init view update1 parseInput
```

<a name='u5rv464dfi6ystqmujtfs4mpxm'/>

### ian.game.UI.view

```unison
ian.game.UI.view uI = case uI of ian.game.UI.UI _ view _ _ -> view
```

<a name='3jm6dxygrldgsgnxj6pbm7pux4'/>

### ian.game.UI.view.modify

```unison
ian.game.UI.view.modify f uI =
  use ian.game.UI UI
  case uI of
    UI init view update parseInput -> UI init (f view) update parseInput
```

<a name='xtos26q5fgjx7otknj3i5lvxsa'/>

### ian.game.UI.view.set

```unison
ian.game.UI.view.set view1 uI =
  use ian.game.UI UI
  case uI of UI init _ update parseInput -> UI init view1 update parseInput
```

<a name='r5qojxh6x4tvyy7ldi37q7axya'/>

### ian.game.chips

```unison
ian.game.chips =
  ian.game.UI.UI
    ian.game.init ian.game.view ian.game.update ian.game.parseGameInput
```

<a name='onfcdmfwvmlwi46pv7dlxhebvu'/>

### ian.game.init

```unison
ian.game.init = ian.game.Model.Model
```

<a name='syltqd63agtx42qlokljtx6yqq'/>

### ian.game.parseGameInput

```unison
ian.game.parseGameInput t =
  use builtin.Universal ==
  if t == "w" then builtin.Either.Right ian.game.Input.Input
  else builtin.Either.Left "Not recognized"
```

<a name='d42enpvm62uistugq37fhjn3ha'/>

### ian.game.playChip

```unison
ian.game.playChip _ = ian.game.run ian.game.chips
```

<a name='yds6zitmtv7aagdtbqunw7gbve'/>

### ian.game.run

```unison
ian.game.run ui =
  use builtin.io printLine
  str = !builtin.io.readLine
  case ian.game.UI.parseInput ui str of
    builtin.Either.Left e ->
      use builtin.Text ++
      printLine ("Invalid input: " ++ e)
    builtin.Either.Right input -> printLine "Valid input!"
```

<a name='t7o7zhxnkh57vg6vu35l5xqdvm'/>

### ian.game.update

```unison
ian.game.update : ian.game.Input -> ian.game.Model -> ian.game.Model
ian.game.update _ m = m
```

<a name='ozy5egc54p3inmcov6kyuzkqji'/>

### ian.game.view

```unison
ian.game.view : ian.game.Model -> builtin.Text
ian.game.view _ = ""
```


