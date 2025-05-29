# Pratica-05
flex
CopiarEditar
%%
%standalone
%unicode

/* Definições de macros */
digito = [0-9]
dia = (0[1-9]|[12][0-9]|3[01])
mes = (0[1-9]|1[0-2])
ano = [0-9]{4}

%%

/* 1) Data no formato dd/mm/aaaa */
{dia}/{mes}/{ano} { 
    System.out.println("Data encontrada: " + yytext());
    return new Token("DATA", yytext());
}

/* 2) Hora no formato hh:mm */
[01][0-9]|2[0-3]:[0-5][0-9] {
    System.out.println("Hora encontrada: " + yytext());
    return new Token("HORA", yytext());
}

/* 3) Número de telefone no formato nn+ (nnn) n nnnn-nnnn */
[0-9]{2}\+[\s]*\([0-9]{3}\)[\s]*[0-9][\s]*[0-9]{4}-[0-9]{4} {
    System.out.println("Telefone encontrado: " + yytext());
    return new Token("TELEFONE", yytext());
}

/* 4) CPF */
[0-9]{3}\.[0-9]{3}\.[0-9]{3}-[0-9]{2} {
    System.out.println("CPF encontrado: " + yytext());
    return new Token("CPF", yytext());
}

/* 5) e-mail */
[\w.-]+@[\w.-]+\.[a-zA-Z]{2,} {
    System.out.println("Email encontrado: " + yytext());
    return new Token("EMAIL", yytext());
}

/* 6) URL */
https?://[\w.-]+(?:/[\w.-]*)* {
    System.out.println("URL encontrada: " + yytext());
    return new Token("URL", yytext());
}

/* Ignorar espaços em branco */
[ \t\n\r]+ {
    // ignora espaços, tabs, novas linhas
}

/* Tratar caracteres não reconhecidos */
. {
    System.out.println("Caractere não reconhecido: " + yytext());
    return new Token("ERROR", yytext());
}

%%

/* Classe Token */
class Token {
    String type;
    String value;
    
    public Token(String type, String value) {
        this.type = type;
        this.value = value;
    }
    
    public String getType() { return type; }
    public String getValue() { return value; }
    
    public String toString() {
        return "Token{" + type + ": " + value + "}";
    }
}
