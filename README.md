# .NET Android Repro

## repro iterator on interface with nullable annotation

```
dotnet build
```

```
obj/Debug/net6.0-android/generated/src/Sentry.Java.Cache.IEnvelopeCache.cs(182,46): warning CS8766: Nullability of reference types in return type of 'IIterator? IEnvelopeCacheInvoker.Iterator()' doesn't match implicitly implemented member 'IIterator IIterable.Iterator()' (possibly because of nullability attributes). [/Users/bruno/temp/repro-android-binding-iterator-issue/repro-android-binding-iterator-issue.csproj]
```

Generates an implementation of Iterator on an interface, with nullability information:

```
IntPtr id_iterator;
public unsafe global::Java.Util.IIterator? Iterator ()
{
    if (id_iterator == IntPtr.Zero)
        id_iterator = JNIEnv.GetMethodID (class_ref, "iterator", "()Ljava/util/Iterator;");
    return global::Java.Lang.Object.GetObject<global::Java.Util.IIterator> (JNIEnv.CallObjectMethod (((global::Java.Lang.Object) this).Handle, id_iterator), JniHandleOwnership.TransferLocalRef);
}
```