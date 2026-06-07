## Description

![Detail](/images/details.png)

## Initial Analysis

According to the challenge description, the objective is to recover the correct username and password required by the program.

This behavior can also be observed in the decompiled code:

```cpp
FUN_1400015a0((basic_ostream<> *)cout_exref,"Enter username: ");
FUN_140001770((basic_istream<> *)cin_exref,(longlong *)&local_78,param_3);

FUN_1400015a0((basic_ostream<> *)cout_exref,"Enter password: ");
FUN_140001770((basic_istream<> *)cin_exref,(longlong *)&local_58,param_3);
```

The program prompts the user for a username and password, storing them in `local_78` and `local_58` respectively.

To improve readability, these variables can be renamed as follows:

```cpp
FUN_140001770((basic_istream<> *)cin_exref,
              (longlong *)&username_input,
              param_3);

FUN_140001770((basic_istream<> *)cin_exref,
              (longlong *)&password_input,
              param_3);
```

## Username Verification

After collecting the username, the program performs the following check:

```cpp
ppppuVar8 = &username_input;

if ((local_68 == 7) &&
   (iVar6 = memcmp(ppppuVar8,"crackme",7),
    iVar6 == 0))
{
    ppppuVar8 = &password_input;
}
```

The user supplied username is compared against the hardcoded string `"crackme"` using `memcmp`.

Since the comparison must succeed for execution to continue, we can determine that the expected username is:

```text
crackme
```

## Password Verification

If the username check succeeds, the program proceeds to validate the password:

```cpp
ppppuVar8 = &password_input;

if ((local_48 == 8) &&
   (iVar6 = memcmp(ppppuVar8,"Rickroll",8),
    iVar6 == 0))
{
    pbVar7 = FUN_1400015a0(
        (basic_ostream<> *)cout_exref,
        "congrats ??");

    std::basic_ostream<>::operator<<(
        pbVar7,
        FUN_140001970);

    system(
        "start https://youtu.be/dQw4w9WgXcQ?si=-WxzNHuzQt6O116t");
}
else
{
    pbVar7 = FUN_1400015a0(
        (basic_ostream<> *)cout_exref,
        "false");
}
```

The password provided by the user is compared against another hardcoded string, `"Rickroll"`.

If the comparison succeeds, the program prints:

```text
congrats ??
```

and launches a browser window that opens the famous Rick Astley music video as a humorous reward for solving the challenge.

If the comparison fails, the program prints:

```text
false
```

This confirms that the expected password is:

```text
Rickroll
```

## Solution

From the recovered string comparisons, the required credentials are:

```text
Username: crackme
Password: Rickroll
```

Providing these values satisfies both validation checks and reaches the success path of the program.


## Output

As we use the extracted username and password we can see we successfully solved the crackme in the output screen.

![Output](/images/output.png)