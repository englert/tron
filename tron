import turtle
import math


# ==========================================
# JÁTÉKABLAK
# ==========================================

ablak = turtle.Screen()
ablak.title("TRON")
ablak.bgcolor("black")
ablak.setup(width=800, height=600)
ablak.tracer(0)


# ==========================================
# JÁTÉK ÁLLAPOTA
# ==========================================

# Lehetséges állapotok:
# "start"
# "countdown"
# "playing"
# "gameover"

allapot = "start"

pont1 = 0
pont2 = 0

jatekos1_el = True
jatekos2_el = True

nyomok1 = []
nyomok2 = []


# ==========================================
# MOTOR 1 - KÉK
# ==========================================

motor1 = turtle.Turtle()

motor1.shape("square")
motor1.color("cyan")

motor1.penup()
motor1.goto(-300, 0)
motor1.setheading(0)

motor1.pensize(4)


# ==========================================
# MOTOR 2 - PIROS
# ==========================================

motor2 = turtle.Turtle()

motor2.shape("square")
motor2.color("red")

motor2.penup()
motor2.goto(300, 0)
motor2.setheading(180)

motor2.pensize(4)


# ==========================================
# SZÖVEG
# ==========================================

szoveg = turtle.Turtle()

szoveg.hideturtle()
szoveg.penup()
szoveg.color("white")


# ==========================================
# PONTSZÁM
# ==========================================

pontszam = turtle.Turtle()

pontszam.hideturtle()
pontszam.penup()
pontszam.color("white")


def pont_kijelzes():

    pontszam.clear()

    pontszam.goto(0, 260)

    pontszam.write(
        f"KÉK: {pont1}       PIROS: {pont2}",
        align="center",
        font=("Arial", 18, "bold")
    )


# ==========================================
# START KÉPERNYŐ
# ==========================================

def start_kepernyo():

    szoveg.clear()

    szoveg.goto(0, 80)

    szoveg.write(
        "TRON",
        align="center",
        font=("Arial", 50, "bold")
    )

    szoveg.goto(0, -10)

    szoveg.write(
        "ENTER = START",
        align="center",
        font=("Arial", 24, "normal")
    )

    szoveg.goto(0, -60)

    szoveg.write(
        "Kék: W A S D     Piros: NYILAK",
        align="center",
        font=("Arial", 16, "normal")
    )

    pont_kijelzes()

    ablak.update()


# ==========================================
# TÁVOLSÁG KÉT PONT KÖZÖTT
# ==========================================

def tavolsag(x1, y1, x2, y2):

    return math.sqrt(
        (x1 - x2) ** 2 +
        (y1 - y2) ** 2
    )


# ==========================================
# ÜTKÖZÉS VIZSGÁLATA
# ==========================================

def utkozik(motor, sajat_nyom, masik_nyom):

    x = motor.xcor()
    y = motor.ycor()


    # --------------------------------------
    # PÁLYA SZÉLE
    # --------------------------------------

    if x < -390 or x > 390:
        return True

    if y < -290 or y > 290:
        return True


    # --------------------------------------
    # SAJÁT KORÁBBI NYOM
    # --------------------------------------

    for px, py in sajat_nyom:

        if tavolsag(x, y, px, py) < 8:
            return True


    # --------------------------------------
    # MÁSIK MOTOR NYOMA
    # --------------------------------------

    for px, py in masik_nyom:

        if tavolsag(x, y, px, py) < 8:
            return True


    return False


# ==========================================
# KÉK MOTOR IRÁNYÍTÁSA
# ==========================================

def motor1_fel():

    if allapot != "playing":
        return

    if motor1.heading() != 270:
        motor1.setheading(90)


def motor1_le():

    if allapot != "playing":
        return

    if motor1.heading() != 90:
        motor1.setheading(270)


def motor1_bal():

    if allapot != "playing":
        return

    if motor1.heading() != 0:
        motor1.setheading(180)


def motor1_jobb():

    if allapot != "playing":
        return

    if motor1.heading() != 180:
        motor1.setheading(0)


# ==========================================
# PIROS MOTOR IRÁNYÍTÁSA
# ==========================================

def motor2_fel():

    if allapot != "playing":
        return

    if motor2.heading() != 270:
        motor2.setheading(90)


def motor2_le():

    if allapot != "playing":
        return

    if motor2.heading() != 90:
        motor2.setheading(270)


def motor2_bal():

    if allapot != "playing":
        return

    if motor2.heading() != 0:
        motor2.setheading(180)


def motor2_jobb():

    if allapot != "playing":
        return

    if motor2.heading() != 180:
        motor2.setheading(0)


# ==========================================
# BILLENTYŰK
# ==========================================

ablak.listen()

# Kék motor
ablak.onkeypress(motor1_fel, "w")
ablak.onkeypress(motor1_le, "s")
ablak.onkeypress(motor1_bal, "a")
ablak.onkeypress(motor1_jobb, "d")

# Piros motor
ablak.onkeypress(motor2_fel, "Up")
ablak.onkeypress(motor2_le, "Down")
ablak.onkeypress(motor2_bal, "Left")
ablak.onkeypress(motor2_jobb, "Right")


# ==========================================
# VISSZASZÁMLÁLÁS
# ==========================================

def visszaszamlalas(szam):

    global allapot

    # Ellenőrizzük, hogy még mindig
    # visszaszámlálásban vagyunk-e
    if allapot != "countdown":
        return


    szoveg.clear()

    szoveg.goto(0, 0)

    szoveg.write(
        str(szam),
        align="center",
        font=("Arial", 70, "bold")
    )

    ablak.update()


    if szam > 1:

        ablak.ontimer(
            lambda: visszaszamlalas(szam - 1),
            1000
        )

    else:

        ablak.ontimer(
            rajt,
            1000
        )


# ==========================================
# RAJT
# ==========================================

def rajt():

    global allapot

    if allapot != "countdown":
        return


    szoveg.clear()

    szoveg.goto(0, 0)

    szoveg.write(
        "RAJT!",
        align="center",
        font=("Arial", 50, "bold")
    )

    ablak.update()


    # Most kezdődik a játék
    allapot = "playing"


    # A "RAJT!" felirat eltűnik
    ablak.ontimer(
        szoveg.clear,
        500
    )


    # Elindul a motor
    ablak.ontimer(
        mozgas,
        500
    )


# ==========================================
# MOZGÁS
# ==========================================

def mozgas():

    global jatekos1_el
    global jatekos2_el

    global pont1
    global pont2

    if allapot != "playing":
        return


    # --------------------------------------
    # MOTOROK MOZGATÁSA
    # --------------------------------------

    if jatekos1_el:
        motor1.forward(4)

    if jatekos2_el:
        motor2.forward(4)


    # --------------------------------------
    # ÚJ POZÍCIÓK ELTÁROLÁSA
    # --------------------------------------

    if jatekos1_el:

        nyomok1.append(
            (motor1.xcor(), motor1.ycor())
        )

    if jatekos2_el:

        nyomok2.append(
            (motor2.xcor(), motor2.ycor())
        )


    # --------------------------------------
    # ÜTKÖZÉS
    # --------------------------------------

    if jatekos1_el:

        if utkozik(
            motor1,
            nyomok1[:-5],
            nyomok2
        ):

            jatekos1_el = False


    if jatekos2_el:

        if utkozik(
            motor2,
            nyomok2[:-5],
            nyomok1
        ):

            jatekos2_el = False


    # --------------------------------------
    # ELLENŐRIZZÜK, HOGY VAN-E GYŐZTES
    # --------------------------------------

    if not jatekos1_el and not jatekos2_el:

        jatek_vege(
            "DÖNTETLEN!"
        )

        return


    if not jatekos1_el:

        pont2 += 1

        jatek_vege(
            "A PIROS MOTOROS NYERT!"
        )

        return


    if not jatekos2_el:

        pont1 += 1

        jatek_vege(
            "A KÉK MOTOROS NYERT!"
        )

        return


    # --------------------------------------
    # KÉPERNYŐ FRISSÍTÉSE
    # --------------------------------------

    ablak.update()


    # --------------------------------------
    # KÖVETKEZŐ MOZGÁS
    # --------------------------------------

    ablak.ontimer(
        mozgas,
        20
    )


# ==========================================
# JÁTÉK VÉGE
# ==========================================

def jatek_vege(uzenet):

    global allapot

    allapot = "gameover"


    szoveg.clear()

    szoveg.goto(0, 40)

    szoveg.write(
        uzenet,
        align="center",
        font=("Arial", 30, "bold")
    )

    szoveg.goto(0, -20)

    szoveg.write(
        "ENTER = ÚJ KÖR",
        align="center",
        font=("Arial", 20, "normal")
    )

    pont_kijelzes()

    ablak.update()


# ==========================================
# ÚJ JÁTÉK
# ==========================================

def uj_jatek():

    global allapot

    global jatekos1_el
    global jatekos2_el

    global nyomok1
    global nyomok2


    # Csak START vagy GAMEOVER állapotban
    # lehet új játékot indítani

    if allapot == "countdown":
        return

    if allapot == "playing":
        return


    # --------------------------------------
    # RÉGI RAJZOK TÖRLÉSE
    # --------------------------------------

    motor1.clear()
    motor2.clear()


    # --------------------------------------
    # MOTOROK KEZDŐHELYZETE
    # --------------------------------------

    motor1.penup()
    motor1.goto(-300, 0)
    motor1.setheading(0)

    motor2.penup()
    motor2.goto(300, 0)
    motor2.setheading(180)


    # --------------------------------------
    # ÚTVONALAK TÖRLÉSE
    # --------------------------------------

    nyomok1 = []
    nyomok2 = []


    # --------------------------------------
    # JÁTÉKOSOK VISSZAÁLLÍTÁSA
    # --------------------------------------

    jatekos1_el = True
    jatekos2_el = True


    # --------------------------------------
    # TOLL VISSZAKAPCSOLÁSA
    # --------------------------------------

    motor1.pendown()
    motor2.pendown()


    # --------------------------------------
    # VISSZASZÁMLÁLÁS INDÍTÁSA
    # --------------------------------------

    allapot = "countdown"

    visszaszamlalas(3)


# ==========================================
# ENTER
# ==========================================

ablak.onkeypress(
    uj_jatek,
    "Return"
)


# ==========================================
# PROGRAM INDÍTÁSA
# ==========================================

start_kepernyo()

ablak.mainloop()
