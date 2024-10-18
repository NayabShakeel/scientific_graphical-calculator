# scientific_graphical-calculator
It is a versatile calculator for students
import numpy as np
import matplotlib.pyplot as plt
import sympy as sp
import streamlit as st
from scipy import stats

def scientific_calculator():
    st.title("Scientific Calculator")

    operation = st.selectbox("Choose an operation", [
        "Addition", "Subtraction", "Multiplication", "Division", 
        "Square Root", "Power", "Logarithm", "Factorial", 
        "Exponential", "Trigonometric Functions", "Inverse Trigonometric Functions", 
        "Hyperbolic Functions"
    ])

    if operation in ["Addition", "Subtraction", "Multiplication", "Division"]:
        num1 = st.number_input("Enter first number", value=0.0)
        num2 = st.number_input("Enter second number", value=0.0)

        if operation == "Addition":
            result = num1 + num2
        elif operation == "Subtraction":
            result = num1 - num2
        elif operation == "Multiplication":
            result = num1 * num2
        elif operation == "Division":
            result = num1 / num2 if num2 != 0 else "Error! Division by zero."

        st.write("Result:", result)

    elif operation == "Square Root":
        num = st.number_input("Enter a number", value=0.0)
        result = np.sqrt(num)
        st.write("Result:", result)

    elif operation == "Power":
        base = st.number_input("Enter base", value=0.0)
        exponent = st.number_input("Enter exponent", value=0.0)
        result = np.power(base, exponent)
        st.write("Result:", result)

    elif operation == "Logarithm":
        num = st.number_input("Enter a number (positive)", value=0.0)
        base = st.selectbox("Choose a base", ["Natural Log (e)", "Base 10"])
        if base == "Natural Log (e)":
            result = np.log(num) if num > 0 else "Error! Input must be positive."
        else:
            result = np.log10(num) if num > 0 else "Error! Input must be positive."
        st.write("Result:", result)

    elif operation == "Factorial":
        num = st.number_input("Enter a non-negative integer", value=0, step=1)
        result = np.math.factorial(num)
        st.write("Result:", result)

    elif operation == "Exponential":
        num = st.number_input("Enter a number", value=0.0)
        result = np.exp(num)
        st.write("Result:", result)

    elif operation == "Trigonometric Functions":
        angle = st.number_input("Enter angle in degrees", value=0.0)
        function = st.selectbox("Choose a function", ["Sine", "Cosine", "Tangent"])
        
        if function == "Sine":
            result = np.sin(np.radians(angle))
        elif function == "Cosine":
            result = np.cos(np.radians(angle))
        elif function == "Tangent":
            result = np.tan(np.radians(angle))

        st.write("Result:", result)

    elif operation == "Inverse Trigonometric Functions":
        value = st.number_input("Enter value", value=0.0)
        function = st.selectbox("Choose a function", ["arcsin", "arccos", "arctan"])
        
        if function == "arcsin":
            result = np.degrees(np.arcsin(value))
        elif function == "arccos":
            result = np.degrees(np.arccos(value))
        elif function == "arctan":
            result = np.degrees(np.arctan(value))

        st.write("Result:", result)

    elif operation == "Hyperbolic Functions":
        angle = st.number_input("Enter angle in degrees", value=0.0)
        function = st.selectbox("Choose a function", ["sinh", "cosh", "tanh"])
        
        if function == "sinh":
            result = np.sinh(np.radians(angle))
        elif function == "cosh":
            result = np.cosh(np.radians(angle))
        elif function == "tanh":
            result = np.tanh(np.radians(angle))

        st.write("Result:", result)

def graphical_calculator():
    st.title("Graphical Calculator")
    
    expression = st.text_input("Enter a function (e.g., x**2, sin(x)):")
    if expression:
        x = sp.symbols('x')
        expr = sp.sympify(expression)
        
        # Generate values
        x_vals = np.linspace(-10, 10, 400)
        y_vals = [expr.subs(x, val) for val in x_vals]

        # Plotting
        plt.figure(figsize=(10, 5))
        plt.plot(x_vals, y_vals, label=str(expr))
        plt.title("Graph of " + str(expr))
        plt.xlabel("x")
        plt.ylabel("f(x)")
        plt.axhline(0, color='black',linewidth=0.5, ls='--')
        plt.axvline(0, color='black',linewidth=0.5, ls='--')
        plt.grid()
        plt.legend()
        st.pyplot(plt)

def main():
    st.sidebar.title("Select Calculator")
    calculator_type = st.sidebar.radio("Choose:", ["Scientific Calculator", "Graphical Calculator"])

    if calculator_type == "Scientific Calculator":
        scientific_calculator()
    else:
        graphical_calculator()

if _name_ == "_main_":
    main()
