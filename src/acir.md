## ACIR (Abstract Circuit Intermediate Representation)

The purpose of ACIR is to act as an intermediate layer between the proof system that Noir chooses to compile to and the Noir syntax.
This separation between proof system and programming language, allows those who want to integrate proof systems to have a stable target, moreover it allows the frontend to compile to any ACIR compatible proof system.

ACIR additionally allows proof systems to supply a fixed list of optimised blackbox functions that the frontend can access. Examples of this would be SHA256, PEDERSEN and SCHNORRSIGVERIFY.

