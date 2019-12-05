# ian table of contents

## Types

+ [ian.cli.mvu.UI](#qgrykkxesr76mivwqlqstavx6i)
+ [ian.game.hardtack.Input](#e67sgwa3rvdw2vptjeksttvszm)
+ [ian.game.hardtack.Model](#hapaw27emmk4sjkdyybchbccue)

## Terms

+ [ian.List.intersperse](#74ppnaeu34ilifb6tzo3thjnim)
+ [ian.List.repeat](#y2ewlwvcwg72c6muzrhodf2zte)
+ [ian.Nat.decrement](#fpjoiazs22643eefindtnlamfa)
+ [ian.cli.mvu.UI.init](#zebbr6laouljh4ymi2rxayy5um)
+ [ian.cli.mvu.UI.init.modify](#w35f4xosbtfolx2hukfdfinu4i)
+ [ian.cli.mvu.UI.init.set](#tqresrkjdfazsayjzhdjbsm7ha)
+ [ian.cli.mvu.UI.parseInput](#3i4qywdjxbmvzy42dvc3dmy424)
+ [ian.cli.mvu.UI.parseInput.modify](#b6d3i3zx3qt3d64dkjf66mbvyi)
+ [ian.cli.mvu.UI.parseInput.set](#znggf5a7gxyiwdhb7ohreqx5tu)
+ [ian.cli.mvu.UI.update](#tyqlbkl6vr6hp5os6cxdmj4nim)
+ [ian.cli.mvu.UI.update.modify](#4vwxkv2b6v3lmn73deybco6mmu)
+ [ian.cli.mvu.UI.update.set](#jdqx3ekoaxfg5dfuwkhd2ilh4y)
+ [ian.cli.mvu.UI.view](#dqq5rcfoizn6kvxzvxtmut2n2i)
+ [ian.cli.mvu.UI.view.modify](#3yxyl7gweqf7nc76jaaxd5r2je)
+ [ian.cli.mvu.UI.view.set](#b6c47qwuvojfythak225bwbiwm)
+ [ian.cli.mvu.run](#6l6rnnf4zsmuiunvynipnpc2ve)
+ [ian.game.hardtack.hardtack](#z7pwuu3wfhrnou2z6oi46qtceu)
+ [ian.game.hardtack.init](#fxgpihq5sujq2lrq3gtt37btxy)
+ [ian.game.hardtack.parseInput](#5ohev42fbawmiy7saahlcvkxeq)
+ [ian.game.hardtack.play](#fypja3772i4kbxnkdewai6pzz4)
+ [ian.game.hardtack.update](#mkjh4ff56egfnauvi3gt34qdj4)
+ [ian.game.hardtack.view](#o4hxg2a6tsfftvo3ehoipwa7o4)

# Types

<a name='qgrykkxesr76mivwqlqstavx6i'/>

### ian.cli.mvu.UI

```unison
unique type ian.cli.mvu.UI model input
  = { init : model,
      view : model -> base.Text,
      update : input -> model -> model,
      parseInput : base.Text -> base.Either base.Text input }
```

<a name='e67sgwa3rvdw2vptjeksttvszm'/>

### ian.game.hardtack.Input

```unison
unique type ian.game.hardtack.Input = North | South | East | West
```

<a name='hapaw27emmk4sjkdyybchbccue'/>

### ian.game.hardtack.Model

```unison
unique type ian.game.hardtack.Model = Model
```


# Terms

<a name='74ppnaeu34ilifb6tzo3thjnim'/>

### ian.List.intersperse

```unison
ian.List.intersperse : a -> [a] -> [a]
ian.List.intersperse separator xs =
  f : [[a]] -> a -> [[a]]
  f acc y =
    use base.List :+
    acc :+ [separator, y]
  case xs of
    [] -> []
    y +: ys -> base.List.join (base.List.foldl f [[y]] ys)
```

<a name='y2ewlwvcwg72c6muzrhodf2zte'/>

### ian.List.repeat

```unison
ian.List.repeat : base.Nat -> a -> [a]
ian.List.repeat n a =
  use base Nat
  f : Nat -> base.Optional (a, Nat)
  f x = base.Optional.map (y -> (a, y)) (ian.Nat.decrement x)
  base.List.unfold n f
```

<a name='fpjoiazs22643eefindtnlamfa'/>

### ian.Nat.decrement

```unison
ian.Nat.decrement n =
  use base.Universal ==
  if n == 0 then base.Optional.None
  else
    use base.Int -
    base.Optional.Some (base.Int.truncate0 (base.Nat.toInt n - +1))
```

<a name='zebbr6laouljh4ymi2rxayy5um'/>

### ian.cli.mvu.UI.init

```unison
ian.cli.mvu.UI.init uI = case uI of ian.cli.mvu.UI.UI init _ _ _ -> init
```

<a name='w35f4xosbtfolx2hukfdfinu4i'/>

### ian.cli.mvu.UI.init.modify

```unison
ian.cli.mvu.UI.init.modify f uI =
  use ian.cli.mvu.UI UI
  case uI of
    UI init view update parseInput -> UI (f init) view update parseInput
```

<a name='tqresrkjdfazsayjzhdjbsm7ha'/>

### ian.cli.mvu.UI.init.set

```unison
ian.cli.mvu.UI.init.set init1 uI =
  use ian.cli.mvu.UI UI
  case uI of UI _ view update parseInput -> UI init1 view update parseInput
```

<a name='3i4qywdjxbmvzy42dvc3dmy424'/>

### ian.cli.mvu.UI.parseInput

```unison
ian.cli.mvu.UI.parseInput uI =
  case uI of ian.cli.mvu.UI.UI _ _ _ parseInput -> parseInput
```

<a name='b6d3i3zx3qt3d64dkjf66mbvyi'/>

### ian.cli.mvu.UI.parseInput.modify

```unison
ian.cli.mvu.UI.parseInput.modify f uI =
  use ian.cli.mvu.UI UI
  case uI of
    UI init view update parseInput -> UI init view update (f parseInput)
```

<a name='znggf5a7gxyiwdhb7ohreqx5tu'/>

### ian.cli.mvu.UI.parseInput.set

```unison
ian.cli.mvu.UI.parseInput.set parseInput1 uI =
  use ian.cli.mvu.UI UI
  case uI of UI init view update _ -> UI init view update parseInput1
```

<a name='tyqlbkl6vr6hp5os6cxdmj4nim'/>

### ian.cli.mvu.UI.update

```unison
ian.cli.mvu.UI.update uI = case uI of ian.cli.mvu.UI.UI _ _ update _ -> update
```

<a name='4vwxkv2b6v3lmn73deybco6mmu'/>

### ian.cli.mvu.UI.update.modify

```unison
ian.cli.mvu.UI.update.modify f uI =
  use ian.cli.mvu.UI UI
  case uI of
    UI init view update parseInput -> UI init view (f update) parseInput
```

<a name='jdqx3ekoaxfg5dfuwkhd2ilh4y'/>

### ian.cli.mvu.UI.update.set

```unison
ian.cli.mvu.UI.update.set update1 uI =
  use ian.cli.mvu.UI UI
  case uI of UI init view _ parseInput -> UI init view update1 parseInput
```

<a name='dqq5rcfoizn6kvxzvxtmut2n2i'/>

### ian.cli.mvu.UI.view

```unison
ian.cli.mvu.UI.view uI = case uI of ian.cli.mvu.UI.UI _ view _ _ -> view
```

<a name='3yxyl7gweqf7nc76jaaxd5r2je'/>

### ian.cli.mvu.UI.view.modify

```unison
ian.cli.mvu.UI.view.modify f uI =
  use ian.cli.mvu.UI UI
  case uI of
    UI init view update parseInput -> UI init (f view) update parseInput
```

<a name='b6c47qwuvojfythak225bwbiwm'/>

### ian.cli.mvu.UI.view.set

```unison
ian.cli.mvu.UI.view.set view1 uI =
  use ian.cli.mvu.UI UI
  case uI of UI init _ update parseInput -> UI init view1 update parseInput
```

<a name='6l6rnnf4zsmuiunvynipnpc2ve'/>

### ian.cli.mvu.run

```unison
ian.cli.mvu.run : ian.cli.mvu.UI model input ->{base.io.IO} ()
ian.cli.mvu.run ui =
  loop m =
    use base.io printLine
    printLine (ian.cli.mvu.UI.view ui m)
    str = !base.io.readLine
    case ian.cli.mvu.UI.parseInput ui str of
      base.Either.Left e ->
        printLine e
        loop m
      base.Either.Right input -> loop (ian.cli.mvu.UI.update ui input m)
  loop (ian.cli.mvu.UI.init ui)
```

<a name='z7pwuu3wfhrnou2z6oi46qtceu'/>

### ian.game.hardtack.hardtack

```unison
ian.game.hardtack.hardtack =
  ian.cli.mvu.UI.UI
    ian.game.hardtack.init
    ian.game.hardtack.view
    ian.game.hardtack.update
    ian.game.hardtack.parseInput
```

<a name='fxgpihq5sujq2lrq3gtt37btxy'/>

### ian.game.hardtack.init

```unison
ian.game.hardtack.init = ian.game.hardtack.Model.Model
```

<a name='5ohev42fbawmiy7saahlcvkxeq'/>

### ian.game.hardtack.parseInput

```unison
ian.game.hardtack.parseInput t =
  use base.Either Right
  use base.Universal ==
  if t == "w" then Right ian.game.hardtack.Input.North
  else
    if t == "s" then Right ian.game.hardtack.Input.South
    else
      if t == "d" then Right ian.game.hardtack.Input.East
      else
        if t == "a" then Right ian.game.hardtack.Input.West
        else base.Either.Left "Not recognized"
```

<a name='fypja3772i4kbxnkdewai6pzz4'/>

### ian.game.hardtack.play

```unison
ian.game.hardtack.play _ = ian.cli.mvu.run ian.game.hardtack.hardtack
```

<a name='mkjh4ff56egfnauvi3gt34qdj4'/>

### ian.game.hardtack.update

```unison
ian.game.hardtack.update :
  ian.game.hardtack.Input -> ian.game.hardtack.Model -> ian.game.hardtack.Model
ian.game.hardtack.update _ m = m
```

<a name='o4hxg2a6tsfftvo3ehoipwa7o4'/>

### ian.game.hardtack.view

```unison
ian.game.hardtack.view : ian.game.hardtack.Model -> base.Text
ian.game.hardtack.view _ =
  use base.Text ++ fromCharList
  use ian.List repeat
  fromCharList (repeat 80 ?-) ++ "\n" ++ fromCharList (repeat 80 ?.)
```


