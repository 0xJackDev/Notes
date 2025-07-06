

This is a reversing file from htb

[haxor@skid rev_lootstash]$ file stash
stash: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=817b1311ae44bdc6ed8a9b563159616844e59c64, for GNU/Linux 3.2.0, not stripped
[haxor@skid rev_lootstash]$


```

undefined8 main(void)

{
  int iVar1;
  time_t tVar2;
  int local_c;
  
  setvbuf(stdout,(char *)0x0,2,0);
  tVar2 = time((time_t *)0x0);
  srand((uint)tVar2);
  puts("Diving into the stash - let\'s see what we can find.");
  for (local_c = 0; local_c < 5; local_c = local_c + 1) {
    putchar(0x2e);
    sleep(1);
  }
  iVar1 = rand();
  printf("\nYou got: \'%s\'. Now run, before anyone tries to steal it!\n",
         *(undefined8 *)(gear + (long)(int)((ulong)(long)iVar1 % 0x7f8 >> 3) * 8));
  return 0;
}
```

Here is the decompiled code. 

It goes over a for loop prints .... And then it prints some seemingly random data
```

[haxor@skid rev_lootstash]$ ./stash
Diving into the stash - let's see what we can find.
.....
You got: 'Fury, Wand of the Summoner'. Now run, before anyone tries to steal it!
[haxor@skid rev_lootstash]$ ./stash
Diving into the stash - let's see what we can find.
.....
You got: 'Shadowfeather, Legacy of the Dead'. Now run, before anyone tries to steal it!
[haxor@skid rev_lootstash]$ ./stash
Diving into the stash - let's see what we can find.
.....
You got: 'Nymph, Cudgel of Secrets'. Now run, before anyone tries to steal it!
[haxor@skid rev_lootstash]$


```


Alright well. they didnt encode their strings this isnt fun. So i just uh Do strings and boom

HTB{n33dl3_1n_a_l00t_stack}
