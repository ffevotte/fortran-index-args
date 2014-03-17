# fortran-index-args.el

## Motivation

Legacy scientific codes written in fortran tend to define subroutines with very
long lists of arguments (in the order of several dozens). When reading and
debugging such code, one often has to count all arguments to the subroutine to
identify the correspondance between an argument in the subroutine definition and
its counterpart in the call.

`fortran-index-args` helps doing this by numbering arguments and showing indexes
before each argument in the list. Such indexes are just displayed on screen, but
do not modify the underlying buffer.

Example ([screencast](http://showterm.io/f5554b8857041dd28dd38#slow)):

```fortran
C Subroutine definition
      SUBROUTINE MCGFLX(SUBFFI,SUBFFA,SUBSCH,CYCLIC,KPSYS,IPRINT,IPTRK,
     1           IFTRAK,IPMACR,NDIM,K,KPN,NLONG,NREG,NSOUT,NG,NGEFF,
     2           NGIND,NZON,MATALB,V,FIMEM,QFR,M,NANI,MAXI,IAAC,KRYL,
     3           ISCR,NMU,NANGL,NMAX,LC,EPSI,CAZ,CPO,ZMU,WZMU,LFORW,
     4           PACA,NFUNL,NMOD,ISGNR,KEYFLX,KEYCUR,SIGAL,LPS,REPS,EPS,
     5           ITST,NCONV,LNCONV,REBFLG,STIS,NPJJM,SOUR,FLUX,LPRISM,
     6           N2REG,N2SOU,NZP,DELU,FACSYM)
C ...
C ...
      END



C Somewhere else in the code: a call to the subroutine
C ...
         CALL MCGFLX(MCGFFI,MCGFFA,MCGDDF,CYCLIC,IBASE(KPSYS),IMPX,
     1           IPTRK,IFTRAK,IPMACR,NDIM,NFI,NUNKNO,NLONG,NBREG,NSOU,
     2           NGRP,NGEFF,IBASE(INGIND),IBASE(INZON),IBASE(MATALB),
     3           BASE(IV),FUNKNO,SUNKNO,NBMIX,NANI,MAXI,IAAC,KRYL,ISCR,
     4           NMU,NANGL,NMAX,LC,EPSI,BASE(ICAZ),BASE(ICPO),BASE(IZMU),
     5           BASE(IWZMU),LFORW,PACA,NFUNL,NMOD,IBASE(ISGNR),
     6           BASE(IKEY),IBASE(KEYCUR),BASE(ISIGAL),LPS,BASE(IREPS),
     7           BASE(IEPS),IBASE(ITST),LBASE(INCONV),LNCONV,REBFLG,
     8           STIS,NPJJM,BASE(IS),BASE(IPHI),LPRISM,N2REG,N2SOU,NZP,
     9           DELU,FACSYM)
C ...
```

## Installation

Just drop `fortran-index-args.el` somewhere and `load` it.

```lisp
(load "/path/to/fortran-index-args.el")
```


## Usage


1. place point in a subroutine arguments list
2. call `M-x fia/display` to display arguments indices
3. call `M-x fia/cleanup` to remove indices and return to the previous view of
   the buffer.

Alternatively, call `M-x fia/toggle` to toggle subroutine arguments indexing.


## Customization

You might want to bind `fia/toggle` to a convenient key. For example:

```lisp
(define-key fortran-mode-map (kbd "C-c i") 'fia/toggle)
```

## License

Copyright (C) 2013 François Févotte.

This program is free software: you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software
Foundation, either version 3 of the License, or (at your option) any later
version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with
this program.  If not, see <http://www.gnu.org/licenses/>.
