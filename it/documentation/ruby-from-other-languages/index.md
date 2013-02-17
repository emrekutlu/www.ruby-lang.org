---
layout: page
title: "Ruby per chi conosce altri linguaggi"
lang: it
---

La prima volta che darai un’occhiata a del codice scritto in Ruby, ti
farà venire in mente altri linguaggi di programmazione che hai già
usato. Questo non è un caso: molti aspetti sintattici risulteranno
familiari a coloro che conoscono Perl, Python e Java (tra gli altri),
quindi se hai già usato uno di questi linguaggi, imparare Ruby sarà
facilissimo.

Questo documento contiene due sezioni principali: la prima descrive che
cosa gli utenti che conoscono altri linguaggi possono aspettarsi quando
proveranno Ruby, mentre la seconda entra un po’ di più nel dettaglio
sulle caratteristiche di Ruby e sul come si possano paragonare a quanto
ti è già familiare.

## Cosa c’è da aspettarsi: Da *Linguaggio X* a Ruby

* [Da C/C++ a
  Ruby](/it/documentation/ruby-from-other-languages/to-ruby-from-c-and-c-/)
* [Da Java a
  Ruby](/it/documentation/ruby-from-other-languages/to-ruby-from-java/)
* [Da Perl a
  Ruby](/it/documentation/ruby-from-other-languages/to-ruby-from-perl/)
* [Da PHP a
  Ruby](/it/documentation/ruby-from-other-languages/to-ruby-from-php/)
* [Da Python a
  Ruby](/it/documentation/ruby-from-other-languages/to-ruby-from-python/)

## Caratteristiche importanti e peculiarità

In questa sezione sono descritte brevemente alcune caratteristiche
particolari di Ruby.

### Iterazione

Due caratteristiche che si discostano da quello che puoi aver già visto
in altri linguaggi sono i “blocchi” e gli iteratori. Invece di iterare
su un indice (come in C, C++, o Java pre-1.5), o su una lista (come il
<tt>for (@a) \{...}</tt> di Perl o il <tt>for i in aList: ...</tt>), con
Ruby vedrai spesso costrutti come:

    una_lista.each do |questo_elemento|
      # Dentro il blocco:
      # facciamo qualcosa con questo_elemento
    end

Per maggiori informazioni su `each` e simili (`collect`, `find`,
`inject`, `sort`, ecc.) vedi `ri Enumerable` (e poi <tt>ri
Enumerable#*nome\_funzione*</tt>).

### Ogni cosa ha un valore

Non c’è differenza tra un’espressione e uno statement: ogni cosa ha un
valore, anche se tale valore è nullo (nil):

    x = 10
    y = 11
    z = if x  true

### I Simboli *non* sono Stringhe!

Molti neofiti di Ruby hannno difficoltà a capire cosa sono i simboli
(Symbols) e a che cosa servono. I simboli possono essere intesi, di
fatto, come degli identificatori usati per riferirsi ad altri oggetti.
Per capire la differenza, prova a scrivere le espressioni seguenti in
`irb`\:

    irb(main):001:0> :pippo.object_id == :pippo.object_id
    => true
    irb(main):002:0> "pippo".object_id == "pippo".object_id
    => false
    irb(main):003:0>

Il metodo `object_id` ritorna l’identità di un’oggetto. Se due oggetti
hanno la stessa `object_id` allora sono di fatto la stessacosa (puntano
entrambi al medesimo oggetto in memoria).

Come puoi vedere, una volta usato un simbolo, qualsiasi altro simbolo
con lo stesso nome si riferirà allo stesso oggetto in memoria, e ognuno
di questi simboli ritornerà quindi la medesima `object_id`.

Diamo un’occhiata più da vicino alle stringhe (“pippo”), nella seconda
espressione: ognuna delle due stringhe ha una propria `object_id`, cioè
mappa un oggetto diverso in memoria. Ciò non avviene con simboli con lo
stesso nome, che puntano sempre al medesimo oggetto. Se sei indeciso se
usare una stringa o un simbolo, pensa a cosa è più importante a seconda
del caso: l’identità di un’oggetto (per esempio una chiave di una Hash)
o il contenuto (“pippo”, nell’esempio precedente).

### Ogni cosa è un oggetto

Questa frase non è un’iporbole: anche classi e numeri interi sono
oggetti, puoi fare con loro le stesse cose che puoi fare con qualsiasi
altro oggetto:

    # Questo è la stessa cosa di:
    # class MyClass
    #   attr_accessor :instance_var
    # end
    MyClass = Class.new do
      attr_accessor :instance_var
    end

### Costanti variabili

Le costanti non sono realmente “costanti”. Se modifichi una costante che
è già stata inizializzata, questo causerà un messaggio di errore, ma non
interromperà l’esecuzione del programma. Tuttavia, questo **non** vuol
dire che tu debba *per forza* ridefinire delle costanti però!

### Convenzioni sui nomi

Ruby usa delle specifiche convenzioni sui nomi dei suoi elementi:

* Se un’identificatore inizia con una maiuscola è una costante
* Se inizia con il simbolo del dollaro ($) è una variabile globale
* Se inizia con `@` è una variabile di istanza
* Se inizia con `@@` è una variabile di classe.

Tuttavia i metodi possono avere un’iniziale maiuscola, anche se questo
può causare confusione, come nell’esempio seguente:

    Costante = 10
    def Costante
      11
    end

In questo modo, `Costante` è 10, ma `Costante()` è 11.

### Finte parole chiave

Ruby non ha delle parole chiave come parametri come Python, tuttavia,
questa funzionalità può essere emulata utilizzando simboli e hash. Qesta
pratica è molto utilizzata in Ruby on Rails.

Esempio:

    def qualche_parola_chiave( parametri )
      params
    end
    qualche_parola_chiave( :parametro_uno => 10, :parametro_due => 42 )
    # => {:parametro_uno=>10, :parametro_due=>42}

### Verità universale

In Ruby ogni cosa eccetto **nil** e **false** è interpretato come
*true*, mentre in C, Python e molti altri linguaggi, 0 e magari anche
altri valori sono interpretati come *false*.

Diamo un’occhiata al seguente codice in Python (questo esempio si
applica anche ad atri linguaggi):

    # in Python
    if 0:
      print "0 è true"
    else:
      print "0 è false"

Questo stamperà “0 is false”, mentre l’equivalente in Ruby:

    # in Ruby
    if 0
      puts "0 è true"
    else
      puts "0 è false"
    end

Stampa “0 è true”.

### I modificatori di accesso si applicano fino alla fine dello scope

Nel seguente codice Ruby:

    class MiaClass
      private
      def un_metodo; true; end
      def un_altro_metodo; false; end
    end

Ci si potrebbe aspettare che `un_altro_metodo` sia pubblico, ma non è
così: il modificatore di accesso ‘private’ continua fino alla fine dello
scope, o fino a quando un altro modificatore di accesso venga
specificato.

I metodi sono pubblici di default:

    class MyClass
      # un_metodo è pubblico
      def un_metodo; true; end
    
      private
    
      # un_altro_metodo è privato
      def un_altro_metodo; false; end
    end

 `public`, `private` e `protected` sono, di fatto, dei metodi, e come tali accettano anche dei parametri. Per modificare la visibilità di un solo metodo, per esempio, è sufficiente passare un simbolo a tale metodo come parametro di un modificatore di accesso per cambiarne la visibilità. ### Accesso ai metodi

In Java, `public` significa che un determinato metodo è accessibile da
tutti. `protected` vuol dire invece che solamente le istanze della
classe o delle sue classi derivate e classi nello stesso package possono
accedere al metodo, e `private` implica che nessuno tranne le istanze
della medesima classe ha accesso al metodo.

Ruby differisce leggermente: `public` vuol dire sempre pubblico, ma
`private` implica che i metodi sono accessibili *solo quando non sono
chiamati con un ricevente esplicito*, solamente **self** può essere
usato come ricevente per una chiamata ad un metodo pubblico.

 `protected` è il più inusuale dei tre. Un metodo protetto può essere chiamato da un’istanza della classe o delle sue derivate, ma anche con un’altra istanza come receiver. Per chiarificare meglio il concetto, consideriamo questo semplice esempio adattato dalle [Ruby FAQ][1]\:     $ irb
    irb(main):001:0> class Test
    irb(main):002:1>   # public per default
    irb(main):003:1*   def func
    irb(main):004:2>     99
    irb(main):005:2>   end
    irb(main):006:1> 
    irb(main):007:1*   def ==(other)
    irb(main):008:2>     func == other.func
    irb(main):009:2>   end
    irb(main):010:1> end
    => nil
    irb(main):011:0> 
    irb(main):012:0* t1 = Test.new
    => #<0x34ab50>
    irb(main):013:0> t2 = Test.new
    => #<0x342784>
    irb(main):014:0> t1 == t2
    => true
    irb(main):015:0> # rendiamo `func` protetto, e viene sempre
    irb(main):016:0* # ritornato true, perchè t2 è pur sempre un'istanza di Test
    irb(main):017:0* class Test
    irb(main):018:1>   protected :func
    irb(main):019:1> end
    => Test
    irb(main):020:0> t1 == t2
    => true
    irb(main):021:0> # Ora rendiamo `func` privato
    irb(main):022:0* class Test
    irb(main):023:1>   private :func
    irb(main):024:1> end
    => Test
    irb(main):025:0> t1 == t2
    NoMethodError: private method `func' called for #<0x342784>
            from (irb):8:in `=='
            from (irb):25
            from :0
    irb(main):026:0></0x342784></0x342784></0x34ab50>

### Classi aperte

 In Ruby, tutte le classi sono “aperte”. Questo vuol dire che puoi aggiungere metodi e variabili e cambiarle in qualsiasi momento, e questo vale anche per classi interne, come `Fixnum` or anche `Object`, il “genitore” di tutti gli oggetti. Ruby on Rails, per esempio, definishe una serie di metodi per fare operazioni temporali con oggetti `Fixnum`\:

    class Fixnum
      def hours
        self * 3600 # numero di secondi in un'ora
      end
      alias hour hours
    end
      
    # 14 ore dalla mezzanotte del primo gennaio 2006
    Time.mktime(2006, 01, 01) + 14.hours # => Sun Jan 01 14:00:00

### Metodi con nomi “strani”

In Ruby, i nomi dei metodi possono terminare con punti esclamativi o
interrogativi. Per convenzione, metodi che rappresentano delle risposte
a delle domande (es. <tt>Array#empty?</tt> ritorna **true** se il
ricevente è vuoto) finiscono con un punto interrogativo, mentre metodi
potenzialmente “pericolosi” (modificano il ricevente o i gli argomenti,
`exit!` ecc.) finiscono, sempre per convenzione, con un punto
esclamativo.

Non tutti i metodi che cambiano i propri argomenti finiscono con un
punto esclamativo, però. Questo è il caso di <tt>Array#replace</tt> che
sostituisce il contenuto di un array con il contenuto di un altro array,
semplicemente perchè non avrebbe molto senso avere un metodo come questo
che non modifica il ricevente.

### Metodi singleton

I metodi singleton sono dei metodi *ad hoc* per singoli oggetti, e sono
pertanto devinibili sull’oggetto per il quale sono stati definiti.

    class Automobile
      def ispeziona
        "Macchina a buon mercato"
      end
    end
    
    porsche = Automobile.new
    porsche.ispeziona # => Macchina a buon mercato
    def porsche.ispeziona
      "Macchina costosa"
    end
    
    porsche.ispeziona # => Macchina costosa
    
    # Gli altri oggetti non sono affetti dalla ridefinizione
    altra_auto = Automobile.new
    altra_auto.ispeziona # => Macchina a buon mercato

### Metodi Mancanti

Ruby non si arrende se non riesce a trovare un metodo che risponde ad un
particolare messaggio, e chiama il metodo `method_missing` con il nome
del metodo non trovato e i relativi argomenti. Di default,
method\_missing causa un’eccezione NameError, ma è possibile ridefinirlo
a seconda delle esigenze di una particolare applicazione, e così fanno
molte librerie. Ecco un esempio:

    # id è il nome del metodo chiamato, l'asterisco
    # fa si che tutti gli argomenti del metodo siano 
    # immagazzinati in un array chiamato 'argomenti'
    def method_missing( id, *argomenti )
      puts "Il metodo #{id} è inesistente - è stato chiamato con " + 
           "i seguenti argomenti: #{argomenti.join(", ")}"
    end
    
    __ :a, :b, 10
    # => l metodo #{id} è inesistente - è stato chiamato 
    # con i seguenti argomenti: a, b, 10

Questo esempio stampa i dettagli della chiamata, ma è possibile gestire
il messaggio nel modo più appropriato, a seconda delle proprie esigenze.

### Scambi di messaggi, non chiamate a funzioni

Una chiamata ad un metodo è, di fatto, un **messaggio** per un altro
oggetto:

    # Questo:
    1 + 2
    # è equivalente a:
    1.+(2)
    # che è lo stesso di
    1.send "+", 2

### I blocchi sono degli oggetti, ma non lo sanno ancora

I blocchi (ma chiamiamoli pure *closure*), sono usati moltissimo nella
libreria standard. Per chiamare un blocco, è possibile usare `yield`
oppure rendere il blocco un oggetto `Proc` aggiungendo un argomento
speciale, così:

    def blocco( &il_blocco )
      # Qui dentro, il_blocco è il blocco passato al metodo:
      il_blocco # ritorna il blocco
    end
    sommatore = blocco { |a, b| a + b }
    # sommatore è ora un oggetto Proc
    sommatore.class # => Proc

È possibile anche creare dei blocchi fuori da chiamate a metodi,
semplicemente chiamando Proc.new con un blocco o chiamando il metodo
`lambda`.

Allo stesso modo, anche i metodi sono pur sempre oggetti:

    method(:puts).call "puts è un oggetto!"
    # => puts è un oggetto!

### Gli operatori sono “zucchero sintattico”

Molti degli operatori sono solamente dello “zucchero sintattico” (con
alcune regole di precendenza però) per delle chiamate a dei metodi. È
possibile, per esempio, ridefinire il metodo ”+” della classe Fixnum:

    class Fixnum
      # Puoi farlo, ma è meglio di no!
      def +( other )
        self - other
      end
    end

Non c’è nemmeno bisogno di usare `operator+`, come in C++.

È è possibile anche definire un modo di accedere a uno specifico
elemento come in un array, definendo i metodi `[]` e `[]=`, mentre per
definire metodi unari + e – (pensa a +1 e -2, ad esempio), bisogna
definire, rispettivamente, i metodi `+@` and `-@`.

I seguenti operatori però **non** sono zucchero sintattico: non sono
metodi e non possono essere ridefiniti:

    =, .., ..., !, not, &&, and, ||, or, !=, !~, ::
{: .code .symbols-code}

Inoltre, +=, \*= ecc. sono solo abbreviazioni di:

 `var = var + other_var`, `var = var * other_var`, ecc. e quindi non possono essere ridefiniti ## Per saperne di più

Quando se pronto per imparare di più su Ruby, dai un’occhiata alla
sezione [Documentazione](/it/documentation/).



[1]: http://www.rubycentral.com/faq/rubyfaq-7.html 