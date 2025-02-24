<!--
* Copyright (c) 2017, 2023 IBM Corp. and others
*
* This program and the accompanying materials are made
* available under the terms of the Eclipse Public License 2.0
* which accompanies this distribution and is available at
* https://www.eclipse.org/legal/epl-2.0/ or the Apache
* License, Version 2.0 which accompanies this distribution and
* is available at https://www.apache.org/licenses/LICENSE-2.0.
*
* This Source Code may also be made available under the
* following Secondary Licenses when the conditions for such
* availability set forth in the Eclipse Public License, v. 2.0
* are satisfied: GNU General Public License, version 2 with
* the GNU Classpath Exception [1] and GNU General Public
* License, version 2 with the OpenJDK Assembly Exception [2].
*
* [1] https://www.gnu.org/software/classpath/license.html
* [2] https://openjdk.org/legal/assembly-exception.html
*
* SPDX-License-Identifier: EPL-2.0 OR Apache-2.0 OR GPL-2.0 WITH
* Classpath-exception-2.0 OR LicenseRef-GPL-2.0 WITH Assembly-exception
-->

# -Xrs

Prevents the Eclipse OpenJ9&trade; runtime environment from handling any internally or externally generated signals such as `SIGSEGV` and `SIGABRT`. Any signals that are raised are handled by the default operating system handlers, which you might want if you are using a debugger such as GDB or WinDbg to diagnose problems in JNI code.

Disabling signal handling in the OpenJ9 VM reduces performance by approximately 2-4%, depending on the application.

:fontawesome-solid-pencil:{: .note aria-hidden="true"} **Note:** Setting this option prevents dumps being generated by the OpenJ9 VM for signals such as `SIGSEGV` and `SIGABRT`, because the VM is no longer intercepting these signals. Do not use the `-Xrs` and [`-XX:+HandleSIGABRT`](xxhandlesigabrt.md) options together. An error is thrown if both options are enabled. To resolve this error, one of the options should be disabled.

## Syntax

        -Xrs
        -Xrs:sync

## Parameters

: If you specify the `sync` parameter:

    - **On AIX&reg;, Linux&reg;, macOS&reg;, and z/OS&reg; systems:** Disables signal handling in the VM for `SIGSEGV`, `SIGFPE`, `SIGBUS`, `SIGILL`, `SIGTRAP`, and `SIGABRT` signals. However, the VM still handles the `SIGQUIT` and `SIGTERM` signals, among others.
    - **On Windows&trade; systems:** Hardware exceptions are not handled by the OpenJ9 VM when this option is specified. However, the Windows CTRL\_BREAK\_EVENT signal, triggered by the Ctrl-Break key combination, is still handled by the VM.

    **Linux and macOS systems** always use the `SIGUSR1` signal.

## See also

- [Signal handling](openj9_signals.md)

<!-- ==== END OF TOPIC ==== xrs.md ==== -->
