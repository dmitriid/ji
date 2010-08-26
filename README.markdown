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
    

See implementation of ArrayListConverter to see how to create a fairly complex converter.  
See implementation of ConversionManager.registerBasic to see how to register your own converters.
