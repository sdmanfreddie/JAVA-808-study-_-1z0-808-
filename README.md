# PROJECT :: java Project mgr


___________________________________________________________________________________________________________________________________________
    BEFORE USING ::
___________________________________________________________________________________________________________________________________________

        1 ) my environment : Fefora 32 + Python 3.8.2 + jdk_14 
        2 ) you can download this file "mybin [ 2020_10_07_14 update ].tar" to get fully project mgr.
            this tar file md5sum is [ 87d041d19795adace126e727710bd81b ]

        about this tool :: $ file /usr/bin/md5sum 
        /usr/bin/md5sum: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter 
        /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=0a05ff65bc9249fea725c08f8489d4edd0bcbcb4, for GNU/Linux 3.2.0, stripped


___________________________________________________________________________________________________________________________________________
    A) ::    how to use projects mgr ? 
___________________________________________________________________________________________________________________________________________

        1 ) add mybin absloute path into ${PATH}. this is not requite. If you do this step, you can run your subproject any where.
        2 ) using "--proj=AZ012E545R888"      to asign sub project
        3 ) using "--file=aquarium/Tank.java" to asign entry point to compile
        4 ) using "--run=aquarium.Tank"       to asign entry point to run


    _______________________________________________________________________________________________________________________________________
    ex A.1 ) :: 
    _______________________________________________________________________________________________________________________________________
            
        if you want run ./mybin/AZ012E545R888 project
              
        follow as $ sh run.sh "--file=aquarium/Tank.java" "--run=aquarium.Tank" "--proj=AZ012E545R888"


    _______________________________________________________________________________________________________________________________________
    ex A.2 ) :: 
    _______________________________________________________________________________________________________________________________________

        if you want run ./mybin/AZ012E545R889 project

        follow as $ sh run.sh "--file=Tank.java" "--run=Tank" "--proj=AZ012E545R889"

    _______________________________________________________________________________________________________________________________________
    ex A.3 ) :: 
    _______________________________________________________________________________________________________________________________________

        if you want run ./mybin/AZ012E545R890 project

        follow as $ sh run.sh "--file=employee/WaterFiller.java" "--run=employee.WaterFiller" "--proj=AZ012E545R890"


    _______________________________________________________________________________________________________________________________________
    ex A.5 ) :: 
    _______________________________________________________________________________________________________________________________________

        if you want run ./mybin/AZ012E545R891 project

        follow as $ sh run.sh "--cp=./my/directory/" "--file=./my/directory/named/A/Bird.java" "--run=named.A.Bird" "--proj=AZ012E545R891"


    _______________________________________________________________________________________________________________________________________
    ex A.6 ) :: how to add your subproject here
    _______________________________________________________________________________________________________________________________________

        step 1 ) : define ./mybin/myProject/Test.java
                
                   import lib.Tool;
	
                   public class Test {
	
                       public static void main ( String[] argu ) {
		
                           try {
			
                               // System.out.println( new Tool( "0123456789" ).getSubString( -1,5 ) );
				
                               System.out.println( new Tool( "0123456789" ).getSubString( 1,5 ) );
				
                           } catch ( Exception e ) {
			
                               e.printStackTrace();
			
                           }
		
                       } // end method main
	
                   } // end class Test


        step 2 ) : define ./mybin/myProject/lib/Tool.java
        
                   package lib;
	
                   public class Tool {
	
                       private String value;
	
                       public Tool ( String v ) {
                       this.value = v;
                       } // end constructor
	
                       public String getSubString( int startPoint, int endPoint ) throws Exception {
		
                           if ( endPoint<startPoint ) throw new Exception ("error 01 : please check range of your sPoint, ePoint :: ");
                           if ( startPoint < 0 ) throw new Exception ("error 02 : startPoint must be > 0 :: ");
                           if ( endPoint>this.value.length()-1 ) throw new Exception ("error 03 : endPoint must be <= str.length() - 1 :: ");
		
                           StringBuffer sb = new StringBuffer();
		
                           for ( int i = startPoint ; i <= endPoint ; i++ ) {
                               sb.append( this.value.charAt( i ) );
                           }
		
                           return sb.toString();
		
                       } // end method 
	
                   } // end class Tool


        step 3 ) : follow as $ sh run.sh "--file=Test.java" "--run=Test" "--proj=myProject"




___________________________________________________________________________________________________________________________________________
  B) ::    how to use jrunscrip ? 
___________________________________________________________________________________________________________________________________________

        1  ) add mybin absloute path into ${PATH}. this is not requite. If you do this step, you can run your subproject any where.
        2  ) using '--import=java.nio.*;'  to add imort                                                     into Test.java
        3  ) using '--content=code here;'  to add code                                                      into Test.java main method
        4  ) using '--function=code here;' to add function                                                  into Test.java
        5  ) using '--classes=code here;'  to add none public ( class | interface | abstract class | enum ) into Test.java
        ps ) jrunscrip not support package in entrypoint Test.java
        ps ) if you want import your lib here, please cp your lib in your own workspace. see ex B.11


    _______________________________________________________________________________________________________________________________________
    ex B.1 ) :: 
    _______________________________________________________________________________________________________________________________________

        if you want run ch01 21.question

        follow as $ 
                
            sh jrunscrip.sh \
            '--classes=class Salmon {
                int count;
                public void Salmon () {
                    count = 4;
                }
                public static void call () {
                    Salmon s = new Salmon();
                    System.out.println( s.count );
                }
            }' \
        '--content=Salmon.call();'


    _______________________________________________________________________________________________________________________________________
    ex B.2 ) :: 
    _______________________________________________________________________________________________________________________________________
            
        sh jrunscrip.sh \
        '--content=
            System.out.println( "hello, man" );
        '


    _______________________________________________________________________________________________________________________________________
    ex B.3 ) :: 
    _______________________________________________________________________________________________________________________________________
		
        sh jrunscrip.sh \
        '--method=
            public static String getter() {
                return "get a fish here ~~~";
            }
        ' \
        '--content=
            System.out.println( getter() );
        '


    _______________________________________________________________________________________________________________________________________
    ex B.4 ) :: 
    _______________________________________________________________________________________________________________________________________
		
        sh jrunscrip.sh \
        '--classes=
            class Book {
                private String name;
                private int    cost;
                Book( String n, int c ) {
                    this.name = n;
                    this.cost = c; 
                }
                public String getName() {
                    return this.name;
                }
                public int    getCost() {
                    return this.cost;
                }
                public String toString () {
                    return "Book( " + this.name + ", " + this.cost + " )";
                }
            } // end class
        ' \
        '--content=
            Book[] books = new Book[] { 
                new Book( "JAVA" , 1000 ) , 
                new Book( "JSP"  , 1500 ) , 
                new Book( "PHP"  , 500  ) 
            };
            Stream<Book> s = Stream.of( books );
            s.filter( ( e ) -> e.getName().contains( "J" ) && e.getCost() > 1000 )
             .forEach( System.out::println );
        '


    _______________________________________________________________________________________________________________________________________
    ex B.5 ) :: 
    _______________________________________________________________________________________________________________________________________
		
        sh jrunscrip.sh \
       '--classes=
            class Book {
                private String name;
                private int    cost;
                Book( String n, int c ) {
                    this.name = n;
                    this.cost = c; 
                }
                public String getName() {
                    return this.name;
                }
                public int    getCost() {
                    return this.cost;
                }
                public String toString () {
                    return "Book( " + this.name + ", " + this.cost + " )";
                }
            } // end class
        ' \
        '--content=
            Book[] books = new Book[] { 
                new Book( "JAVA" , 1000 ) , 
                new Book( "JSP"  , 1500 ) , 
                new Book( "PHP"  , 500  ) 
            };
            Stream<Book> s = Stream.of( books );
            System.out.println(
                s.filter( ( e ) -> e.getName().contains( "J" ) && e.getCost() > 1000 )
                 .findFirst().get()
            );
        '


    _______________________________________________________________________________________________________________________________________
    ex B.6 ) :: 
    _______________________________________________________________________________________________________________________________________
		
        sh jrunscrip.sh \
        '--content=
            for ( String s : argus ) {
                System.out.println( "s >> " + s );
            }
        ' \
        '--argu=String[] argus'


    _______________________________________________________________________________________________________________________________________
    ex B.7 ) :: 
    _______________________________________________________________________________________________________________________________________
		
        sh jrunscrip.sh \
        '--content=
            for ( String s : argus ) {
                System.out.println( "s >> " + s );
            }
        ' \
        '--argu=String[] argus' \
        '--jargu=1 2 3' \
        '--jargu=4 5 6'


    _______________________________________________________________________________________________________________________________________
    ex B.8 ) :: 
    _______________________________________________________________________________________________________________________________________
		
        sh jrunscrip.sh \
        '--argu=String... argus'


    _______________________________________________________________________________________________________________________________________
    ex B.9 ) :: 
    _______________________________________________________________________________________________________________________________________

        sh jrunscrip.sh '--field=boolean[] ary = new boolean[2];'
                        '--content=System.out.println( new Test().ary[0] );'


    _______________________________________________________________________________________________________________________________________
    ex B.10 ) :: 
    _______________________________________________________________________________________________________________________________________

        sh jrunscrip.sh '--content=int[] ary = new int[2];
                                   System.out.println( ary[0] );'


    _______________________________________________________________________________________________________________________________________
    ex B.11 ) :: 
    _______________________________________________________________________________________________________________________________________

        ps ) : workspace is ~/work/
                
             : my own lib in here pash : ~/work/lib/Tool.java

             : run as follows $ sh jrunscrip.sh '--import=import lib.Tool;' \
                                                '--content=try{
                                                                System.out.println( new Tool( "0123456789" ).getSubString( 1,5 ) );
                                                           } catch ( Exception e ) {}
                                                '



___________________________________________________________________________________________________________________________________________
  C) ::    how to back mybin ?
___________________________________________________________________________________________________________________________________________

        STEP 1 ) cd to ./mybin 
        STEP 2 ) run cmd as follows : $ python3 back.py
                 it will use system time to create a tar file such as follow : mybin[2020_10_07_13_32].tar



___________________________________________________________________________________________________________________________________________
  D) ::    how to restore mybin ?
___________________________________________________________________________________________________________________________________________

        STEP 1 ) cd to ./mybin 
        STEP 2 ) run cmd as follows : $ python3 restore.py 
                 it will use tar file like this mybin[2020_10_07_13_32].tar, 
                 it will use the newest mybin[_system_].tar to restore


