Functors, Applicatives, And Monads In Pictures
=======================================

���� : http://adit.io/posts/2013-04-17-functors,_applicatives,_and_monads_in_pictures.html

 ����, �ܼ��� ��(value)�� �ֽ��ϴ�.

![value.png]

```haskell
Prelude> 2
2
```

 �׸���, �츮�� �Լ��� �� ���� �����Ű�� ���� �˰� �ֽ��ϴ�.

![value_apply.png]

```haskell
Prelude> (+3) 2
5
```

 ���� �����մϴ�. �׷� ����, ��� ����(context)�� ���� ����ִٰ� �����غ��ô�. ���� ��������, ���� ���� �� �ִ� ��� ���¸� ���ڶ�� ���� �� ���� ���Դϴ�.


![value_and_context.png]

```haskell
Prelude> Just 2
Just 2
```

 ����, �� ���� �Լ��� �����ϰ� �Ǹ�, __���¿� ����__ �ٸ� ����� ��� �� ���Դϴ�.
 
 Functors, �̸� ��������� ����(idea) �߿��� Applicatives, Monads, Arrows ����� �ֽ��ϴ�. `Maybe` ������ Ÿ���� �ΰ��� ���·� ������ �� �ֽ��ϴ�.

![context.png]

```haskell
data Maybe a = Nothing | Just a
```

```haskell
Prelude> :type Just
Just :: a -> Maybe a

Prelude> :type Nothing
Nothing :: Maybe a
```

 ��������, `Just a`�� `Nothing`�� ����, �Լ��� ��� ����Ǵ��� ������ �ϰڽ��ϴ�. �켱, Functors�� ���� ������ ������ �ϰڽ��ϴ�.

# Functors

 ���ڿ� ���� ����, ����� �Լ��� ������ ���� �����ϴ�.

![no_fmap_ouch.png]

```haskell
Prelude> (+3) (Just 2)
 ERR - No instance for (Num (Maybe a0))
```

 `fmap`�� ��Ÿ� ����̸�, ���ڿ� ���ؼ� �����մϴ�. `fmap`�� ���ڿ� �ִ� ���� ��� �Լ��� �����ؾ� ������ �˰� �ֽ��ϴ�. ���� ���, `Just 2`�� `(+3)`�� ������� ���ô�. `fmap`�� �̿��غ���, 

```haskell
> fmap (+3) (Just 2)
Just 5
```

![fmap_apply.png]

 __��!__ `fmap`�� ������ �س½��ϴ�. ��� `fmap`�� �Լ��� �����Ű�� ���� �˰� �ִ� �ɱ��?



# Functor�� ����ü ���ϱ�?

 `Functor`�� [typeclass]�Դϴ�. ���� ���ǰ� �����ֽ��ϴ�.
 
![functor_def.png]

 `Functor`�� fmap�� �����Ű�� ����� ������ ������ Ÿ���Դϴ�. ����, ��� fmap�� �����ϴ����� ���� �ֽ��ϴ�.

![fmap_def.png]

 ����, ����� ������ ���� �� �� �ֽ��ϴ�.

```haskell
> fmap (+3) (Just 2)
Just 5
```

 `Maybe`���� `Functor`�̱⿡, `fmap`�� �������� ���� �Լ��� �����Ͽ����ϴ�. ��������, `Just`�� `Nothing`�� ���� `fmap`�� �����Ű�� ����� ���� �����ֽ��ϴ�.

```haskell
instance Functor Maybe where  
    fmap func (Just val) = Just (func val)
    fmap func Nothing = Nothing 
```

 ����, `fmap (+3) (Just 2)`�̶�� ������, �ڿ��� ��� ���� �߻��ϴ����� �����ֽ��ϴ�.
 
![fmap_just.png]


 �׷���, `(+3)`�� `Nothing`�� ������� ������ �ϰڽ��ϴ�.

![fmap_nothing.png]

```haskell
> fmap (+3) Nothing
Nothing
```

![bill.png]

_Maybe functor�� �𸣴� Bill O��Reilly_

 ��Ʈ������ ���Ǿó��, `fmap`�� ������ �ؾ����� �˰� �ֽ��ϴ�. `Nothing`���� �����ϸ�, `Nothing`���� ������! `fmap`�� zen(��, �������� ��)�Դϴ�. ����, `Maybe` ������ Ÿ���� �� �����ϴ��� ������ ���ô�. �������, `Maybe`�� ���� ����, ������ ����� ������ �۾��� �Ѵٸ�,

```ruby
post = Post.find_by_id(1)
if post
  return post.title
else
  return nil
end
```

������, Haskell�� ������ ���� �� �� �ֽ��ϴ�.

```hakskell
fmap (getPostTitle) (findPost 1)
```

 ����, `findPost`�� �Խñ�(post)�� ��ȯ�Ѵٸ�, `getPostTitle`�� ����(title)�� ���� ���Դϴ�. `Nothing`�� ��ȯ�ϸ�, `Nothing`�� ���� ���Դϴ�. �ſ� �������� �ʽ��ϱ�? `fmap`�� ����ǥ��(infix) ������ `<$>`�̸�, ������ ���� ���⵵ �մϴ�.

```haskell
getPostTitle <$> (findPost 1)
```

 ����, �� �ٸ� ���� �ֽ��ϴ�. ����Ʈ�� �Լ��� �����Ű�� �������� ���������?

![fmap_list.png]

 ����Ʈ ���� functor���� ���̿����ϴ�! ���� ���ǰ� �����ֽ��ϴ�.

```haskell
instance Functor [] where
    fmap = map
```

 ��, ��, ���������� �ϳ� ��. �Լ��� �� �ٸ� �Լ��� �����Ű�� ���� ���� ���������?

```haskell
fmap (+3) (+1)
```

```haskell
Prelude> :type fmap (+3) (+1)
fmap (+3) (+1) :: (Functor ((->) b), Num b) => b -> b
```

 ���� �ϳ��� �Լ��� �ֽ��ϴ�.

![function_with_value.png]

 �Լ��� �� �ٸ� �Լ��� ������ ������ �ϰڽ��ϴ�.

![fmap_function.png]

 ��� ���� �Լ� �Դϴ�.

```haskell
> import Control.Applicative
> let foo = fmap (+3) (+2)
> foo 10
15
```

 ����, �Լ� ���� Functor�Դϴ�.

```haskell
instance Functor ((->) r) where  
    fmap f g = f . g
```

 �Լ��� fmap�� ����ϸ�, function composition�� �ѰͰ� �����ϴ�.



# Applicatives

 ���� �ܰ�� �Ѿ������ �ϰڽ��ϴ�. Functors���� ���Դ� ��ó��, ���ڿ� ���� �ֽ��ϴ�.

![value_and_context.png]

 �Լ� ���� ���ڿ� �� �� �ֽ��ϴ�.

![function_and_context.png]


 �׷� �ڼ��� ���캸���� �ϰڽ��ϴ�. Applicatives�� �ٺ��� �ƴմϴ�. Control.Applicative�� ���� �� ����, ���� �� �Լ��� �����ϴ� ���� �˵��� `<*>`�� �����߽��ϴ�.
 
![applicative_just.png]

 ��, ������ ���� �� �� �ֽ��ϴ�.

```haskell
Just (+3) <*> Just 2 == Just 5
```

 `<*>`�� ����ϸ� ���� ��̷ο� ����� ���� �� �ֽ��ϴ�. ����,

```haskell
> [(*2), (+3)] <*> [1, 2, 3]
[2, 4, 6, 4, 5, 6]
```

![applicative_list.png]

 ����, Functor�δ� �� �� ������, Applicative�� �� �� �ִ°� �����ֽ��ϴ�. �ΰ��� ���ڸ� ���ϴ� �Լ���, ��� �ӿ� ���� ����ִ� �ΰ��� ���ڿ� �����ų���?

```haskell
> (+) <$> (Just 5)
Just (+5)
> Just (+5) <$> (Just 4)
ERROR ??? WHAT DOES THIS EVEN MEAN WHY IS THE FUNCTION WRAPPED IN A JUST
```

 Applicatives:

```haskell
> (+) <$> (Just 5)
Just (+5)
> Just (+5) <*> (Just 3)
Just 8
```
 `Applicative`�� `Functor`�� ������ ���ĳ��鼭 "��� ���� ���ڵ��� �ٷ� �� �ִ� �Լ��� ���ܴ�.".

 "`<$>`�� `<*>`�� ������, ���ڿ� ����ִ� ������, ���ڸ� ���� �� �� ���� �Լ��� �Ѱ��༭, �ӿ� ���� ����ִ� ���ڸ� ���� �� �ִٰ�! ��������!"

```haskell
> (*) <$> Just 5 <*> Just 3
Just 15
```

![TaTdV.gif]

_functor�� �Լ��� �����Ű�� ���� ���Ѻ��� �ִ� applicative_

 ���! ���� ������ ���� �ϴ� `liftA2`�� �ֽ��ϴ�.

```haskell
> liftA2 (*) (Just 5) (Just 3)
Just 15
```

# Monads

�𳪵带 ���� ��� :

1. ��ǻ�� ���� �ڻ������� ����.
2. �ʿ������ ���� ġ���!

Monads�� ���ο� �ع��� �����Ͽ����ϴ�.
 
Functors�� ���ڿ� �ִ� ���� �Լ��� ������ �� �ֽ��ϴ�.

![fmap.png]

Applicatives�� ���ڿ� �ִ� ����, ���ڿ� �ִ� �Լ��� ���� �� �� �ֽ��ϴ�.

![applicative.png]

 Monads�� ���ڿ� �ִ� ���� �Լ��� ������� __���� ����ִ� ���ڸ� ��ȯ__�� �� �ֽ��ϴ�.
 
 Monads�� �̷��� ���� ó���ϴ� ("bind"�� �Ҹ���) `>>=`��� �Լ��� ������ �ֽ��ϴ�.

 ������ ��ǥ���ô�. �������� ���Դ� `Maybe`�� �𳪵��Դϴ�.

![context.png]

_����ִ� Just a �𳪵�_

 ¦���� ���ؼ��� �����ϴ� �Լ�, `half`�� �ִٰ� �����غ��ô�.

```haskell
half x = if even x
           then Just (x `div` 2)
           else Nothing
```

![half.png]


 ���� ����ִ� ���ڸ� ������ ��� �ɱ��?

![half_ouch.png]

 �Լ��� ���� ����ִ� ���ڸ� �о� ��������, `>>=`�� �ʿ��մϴ�. ����, `>>=`�� ������ �ֽ��ϴ�.

![plunger.jpg]

 ��� �����ϴ��� Ȯ���� ���ô�.
 
```haskell
> Just 3 >>= half
Nothing
> Just 4 >>= half
Just 2
> Nothing >>= half
Nothing
```

 ���ο��� ����� ������ �ɱ��? `Monad`�� �� �ٸ� [typeclass]�Դϴ�. ����, ���� �� �Ϻΰ� �����ֽ��ϴ�.

```haskell
class Monad m where    
    (>>=) :: m a -> (a -> m b) -> m b  
```

`>>=`��,

![bind_def.png]

 ����, `Maybe`�� Monad�Դϴ�:

```haskell
instance Monad Maybe where
    Nothing >>= func = Nothing
    Just val >>= func  = func val
```


����, `Just 3`�� �� �� ��� �����ϴ��� �����ֽ��ϴ�!

![monad_just.png]

 `Nothing`�� ������ ���� �ܼ��� ���ϴ�.

![monad_nothing.png]

 �̷��� ���޾� �θ� ȣ���� �� �� �ֽ��ϴ�.

```haskell
> Just 20 >>= half >>= half >>= half
Nothing
```

![monad_chain.png]

![whoa.png]


 �����ݴϴ�. ���� �츮�� `Maybe`�� Functor����, Applicative�̸�, Monad��� ���� �˰� �Ǿ����ϴ�.

 ���� ����, `IO` �𳪵� ������ �� ���ڽ��ϴ�.

![io.png]

_���� 10�ƴ�... ���� IO��_

 ������ Ư���� �Լ��� �ֽ��ϴ�. `getLine`�� ���ڸ� ���� �ʰ�, ������� �Է��� �޽��ϴ�.

![getLine.png]

```haskell
getLine :: IO String
```

 `readFile`�� ���ڿ�(���ϸ�)�� �޾�, ���Ͽ� �ִ� ������ ��ȯ�մϴ�.
 
![readFile.png]

```haskell
readFile :: FilePath -> IO String
```

 `putStrLn`�� ���ڿ��� �޾� ����մϴ�.

![putStrLn.png]

```haskell
putStrLn :: String -> IO ()
```

 ���� ���� ������ �Լ��� ����� ��(Ȥ�� ���ų�)�� �޾Ƽ�, ���� ����ִ� ���ڸ� ��ȯ�մϴ�. ����, �츮�� �̸� `>>=`�� ���� �� �ֽ��ϴ�!

![monad_io.png]

```haskell
getLine >>= readFile >>= putStrLn
```

 �� ��! �𳪵� � ���������ϴ�!

 �������ڸ�, Haskell�� �� �𳪵忡 ����, `do`��� syntax suger�� ������ �־����ϴ�.

```haskell
foo = do
    filename <- getLine
    contents <- readFile filename
    putStrLn contents
```

# Conclusion

1. functor�� `Functor` Ÿ�� Ŭ������ ������ ������ Ÿ���̴�.
2. applicative�� `Applicative` Ÿ�� Ŭ������ ������ ������ Ÿ���̴�.
3. monad�� `Monad` Ÿ�� Ŭ������ ������ ������ Ÿ���̴�.
4. `Maybe`�� �� ������ ��� ���������Ƿ�, functor���� applicative�̸� monad�̴�.

 �� ���� �������� �����ϱ�?

![recap.png]

* functors: `fmap`�̳� `<$>`�� �̿��Ͽ� ���� �� ���� �Լ��� ������ �� �ִ�.
* applicatives: `liftA`�� `<*>`�� �̿��Ͽ� ���� �� �Լ��� ���� �� ���� ������ �� �ִ�.
* monads: `liftM`�� `>>=`�� �̿��Ͽ� ���� ����ִ� ���ڸ� �޾� �Լ��� �����ϰ� ���� ����ִ� ���ڸ� ��ȯ�� �� �ִ�.

 �츮 ��� �𳪵��� ���� ���� ���� ����(Ʈ���̵� ��ũ)�̶�� �Ϳ� ����, �����Ѵٰ� �����մϴ�. �� ���̵�� �����ϱ⿣ ���� �̸��ϴ�. [LYAH��s section on Monads]�� Ȯ���Ͻñ� �ٶ��ϴ�. Miran�� ���� �̹� �𳪵忡 ���� ���, �Ǹ��� ���� �س±⿡, ���� ���� ���� ��������� �Ѿ���ϴ�.

 [���þ� ����](http://habrahabr.ru/post/183150/)�� �ֽ��ϴ�. �� ���� �𳪵�� �׸��� ���ϽŴٸ�, [three useful monads]�� Ȯ���Ͻñ� �ٶ��ϴ�.



 [value.png]: ./img/value.png
 [value_apply.png]: ./img/value_apply.png
 [value_and_context.png]: ./img/value_and_context.png
 [context.png]: ./img/context.png
 [no_fmap_ouch.png]: ./img/no_fmap_ouch.png
 [fmap_apply.png]: ./img/fmap_apply.png
 [functor_def.png]: ./img/functor_def.png
 [fmap_def.png]: ./img/fmap_def.png
 [fmap_just.png]: ./img/fmap_just.png
 [fmap_nothing.png]: ./img/fmap_nothing.png
 [fmap_list.png]: ./img/fmap_list.png
 [function_with_value.png]: ./img/function_with_value.png
 [fmap_function.png]: ./img/fmap_function.png
 [function_and_context.png]: ./img/function_and_context.png
 [applicative_just.png]: ./img/applicative_just.png
 [applicative_list.png]: ./img/applicative_list.png
 [fmap.png]: ./img/fmap.png
 [applicative.png]: ./img/applicative.png
 [half.png]: ./img/half.png
 [half_ouch.png]: ./img/half_ouch.png
 [bind_def.png]: ./img/bind_def.png
 [monad_just.png]: ./img/monad_just.png
 [monad_nothing.png]: ./img/monad_nothing.png
 [monad_chain.png]: ./img/monad_chain.png
 [whoa.png]: ./img/whoa.png
 [io.png]: ./img/io.png
 [getLine.png]: ./img/getLine.png
 [readFile.png]: ./img/readFile.png
 [putStrLn.png]: ./img/putStrLn.png
 [monad_io.png]: ./img/monad_io.png
 [recap.png]: ./img/recap.png
 

 [bill.png]: ./img/bill.png 
 [TaTdV.gif]: ./img/TaTdV.gif
 [plunger.jpg]: ./img/plunger.jpg


 [typeclass]: http://learnyouahaskell.com/types-and-typeclasses#typeclasses-101
 [function composition]:  http://en.wikipedia.org/wiki/Function_composition
 
 [three useful monads]: http://adit.io/posts/2013-06-10-three-useful-monads.html
 [LYAH��s section on Monads]: http://learnyouahaskell.com/a-fistful-of-monads