from pyparsing import Word, alphas, OneOrMore, Optional, Group, Suppress

# Define grammar for simple arithmetic expressions
expr = Word(alphas) + Optional(Suppress('(') + Group(expr) + Suppress(')'))
arith_expr = OneOrMore(expr)

# Parse DSL input
dsl_input = "add(subtract(10, 5), multiply(3, 4))"
parsed = arith_expr.parseString(dsl_input)

# Interpret parsed DSL
def interpret(parsed):
    operator = parsed[0]
    operands = parsed[1:]
    if operator == "add":
        return sum(operands)
    elif operator == "subtract":
        return operands[0] - operands[1]
    elif operator == "multiply":
        return operands[0] * operands[1]
    else:
        raise ValueError(f"Unknown operator: {operator}")

# Evaluate and print the result
result = interpret(parsed)
print("Result:", result)
