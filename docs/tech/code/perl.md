# Perl

## Adding modules without root

```
$ wget -O- http://cpanmin.us | perl - -l ~/perl5 App::cpanminus local::lib 
$ eval `perl -I ~/perl5/lib/perl5 -Mlocal::lib` 
$ echo 'eval `perl -I ~/perl5/lib/perl5 -Mlocal::lib`' >> ~/.profile 

$ cpanm --interactive -v Mail::Sendmail # Install modules using cpanm 
```

Add this in your code:&#x20;

```
use local::lib q(~/perl5); 
```

Everything will be in \~/perl5 (which can be copied to another host)&#x20;



Alternatively:&#x20;

```
$ perl -MCPAN -e shell 
```

