This is a simple and some what dumb library to facliltate conversion between custom Java types and Erlang.

    
    CoversionManager cm = new ConversionManager();
    
    // loads basic convertors for integers, booleans, 
    // strings and the like
    cm.registerBasic(); 
    
    ArrayList arr = new ArrayList();
    arr.add("hello");
    arr.add(10);
    
    OtpErlangList list = cm.convert(arr);
    // if you send this list over to Erlang, you'll get
    // ["hello", 10] 
    

A basic usage would be something like this:

    ConversionManager cm = new ConversionManager();
    cm.registerBasic();

    cm.register(
        new MyCustomConverter1(),
        new MyCustomConverter2(),
        new MyCustomConverter3()
    );

    OtpNode self = new OtpNode("node@localhost");
    OtpMbox mbox = self.createMbox("mbox");
    
    while(true) {
        Object o = o = mbox.receive();
        
        Object result = do_something_horrible(o);
        OtpErlangObject out = cm.convert(result);

        mbox.send(from, out);
    }

See implementation of ArrayListConverter to see how to create a fairly complex converter.  
See implementation of ConversionManager.registerBasic to see how to register your own converters.


