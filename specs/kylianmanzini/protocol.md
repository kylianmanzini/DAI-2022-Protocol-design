Protocol objectives: what does the protocol do?

The SUS protocole communicate between a client and a server. Basicly the client sent a string with 
operations and the server send back the response. This protocole MUST work with +-*/ and COULD work with 
parentesis operation.

Overall behavior:
What transport protocol do we use?
    TCP
How does the client find the server (addresses and ports)?
    Ip address and the port 12345
Who speaks first?
    Serveur
Who closes the connection and when?
    Server, when sending result or error

Messages:
What is the syntax of the messages?
    S : OP BASICOP / PARENTESIS END
    C : CALC "operationStringTreated" END
    S : RESULT num END
    S : ERROR errorCode errorTxt END
    S : QUIT END

What is the sequence of messages exchanged by the client and the server? (flow)
    OP 
    CALC
    RESULT / ERROR
    QUIT

What happens when a message is received from the other party? (semantics)
    result or error if server receive from client

Specific elements (if useful)
Supported operations
    + - * / and ()
Error handling

    S : ERROR errorCode errorTxt END

    ERROR LIST :
    400 - WSYNTAX
    401 - UKNOWNOP
    601 - DIV0
    602 - WRONGPAR

Extensibility

Examples: examples of some typical dialogs.

    S : OP BASICOP END
    C : CALC "3+5*2" END
    S : RESULT 13 END
    S : QUIT END

    S : OP BASICOP END
    C : CALC "3-(2*(3))" END
    S : ERROR 401 UKNOWNOP END
    S : QUIT END

    S : OP BASICOP PARENTESIS END
    C : CALC "3-(2*(3))" END
    S : RESULT -3 END
    S : QUIT END

    S : OP BASICOP PARENTESIS END
    C : CALC "(((((3+2)" END
    S : ERROR 602 WRONGPAR END
    S : QUIT END

    S : OP BASICOP END
    C : RTVDF >retGFDGD
    S : ERROR 400 WSYNTAX END
    S : QUIT END