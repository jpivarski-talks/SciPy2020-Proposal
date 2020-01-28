# SciPy 2020 Proposal

   * [Conference website](https://www.scipy2020.scipy.org/)
   * [Submission instructions](https://www.scipy2020.scipy.org/talk-poster-presentations)
   * [Matthew's example from last year](https://github.com/matthewfeickert/SciPy2019-Proposal#readme)
   * [SciPy 2019 talks and abstracts](https://www.youtube.com/playlist?list=PLYx7XA2nY5GcDQblpQ_M1V3PQPoLWiDAC)

## Authors

| Name | Email | Country | Organization | Web page | Corresponding? |
|:-:|:-:|:-:|:-:|:-:|:-:|
| Jim Pivarski | _(princeton.edu)_ | United States | Princeton University | _(none)_ | **yes** |
| Ianna Osborne | _(cern.ch)_ | Switzerland | Princeton University | _(none)_ | no |
| Peter Elmer | _(cern.ch)_ | United States | Princeton University | _(none)_ | no |

## Title

**Awkward Array: Manipulating JSON-like Data with NumPy-like Idioms**

_(In the 2019 program, talks about a software library had this form: library name, colon, short description, most words capitalized.)_

## The Short Summary

_(The brief description which will appear in the online program and give attendees a basic sense of your talk. This should be around 100 words or less.)_

NumPy simplifies and accelerates mathematical calculations in Python, but only for rectilinear arrays of numbers. Awkward Array provides a similar interface for JSON-like data: slicing, masking, broadcasting, and performing vectorized math on the attributes of objects, unequal-length nested lists (i.e. ragged/jagged arrays), and heterogeneous data types. Awkward Arrays are columnar data structures, like (and convertible to/from) Apache Arrow, with a focus on manipulation, rather than serialization/transport. These arrays can be passed between C++ and Python, and they can be used in functions that are JIT-compiled by Numba.

_(84 words.)_

## Audience

_(Who is the intended audience for your talk?)_

This talk is intended for data analysts, particularly those who are involved in cleaning data from complex sources, as well as developers who might want to collaborate.

_(What, specifically, will attendees learn from your talk?)_

They will learn how to manipulate nested data structures using vectorized functions on examples drawn from semi-regular JSON. They will also see a little of how the machinery works.

## The Abstract

_(Your placement in the program will be based on reviews of your abstract. This should be a roughly 500 word outline of your presentation. This outline should concisely describe software of interest to the SciPy community, tools or techniques for more effective computing, or how scientific Python was applied to solve a research problem. A traditional background/motivation, methods, results, and conclusion structure is encouraged but not required. Links to project websites, source code repositories, figures, full papers, and evidence of public speaking ability are encouraged.)_

### Introduction and motivation

Particle physicists routinely have to manipulate large numbers of complex objects that represent hierarchical particle decays. Looping over combinations of particles to find candidates that match a given topology is not a preprocessing step or a cleaning step: it _is_ the analysis. This combination of complexity and large datasets has made it difficult for particle physicists to use Python's standard data analysis tools, such as NumPy, Pandas, and xarray.

Awkward Array was introduced in September 2018, and it has become the basis for a new Python-based ecosystem in our field, including the Scikit-HEP project (https://scikit-hep.org) and PyHEP series of conferences, the third of which will be co-located with SciPy 2020 (https://indico.cern.ch/event/882824). However, there's nothing domain-specific about this intersection of complex data with big data.

After presenting the complexity problem from a particle physics perspective, I would introduce the Awkward Array library by applying it to GeoJSON map files, which already have enough structure to justify why one would want to slice, mask, and vectorize calculations with Awkward Array.

### Columnar data

Just as NumPy's contiguous data structure is key to its performance, Awkward Array relies upon columnar data to be fast and memory-efficient. It may not be obvious how nested, variable-length data can be expressed in a columnar form, so I would take some time to show the layout of columnar data structures and how we can manipulate them without converting them into objects and without copying all of the internal buffers.

### Enumerating over combinations

In particle physics, we often need to iterate through combinations of two or more objects from different collections, so Awkward Array has vectorized functions for building per-element Cartesian products and pairs or triples without replacement. These turn out to be the cross-join and inner-join operations of SQL, but applied independently to each index of a set of arrays, as though every array element were an SQL table.

### Creating Awkward Arrays

It's not enough to manipulate data structures; sometimes they need to be generated from scratch. Awkward Arrays can be appended to, but not changed in place. Our interface for filling arrays also determines their type dynamically, from the order and choice of fill commands.

### C++ and Numba interfaces

Awkward Array is implemented in C++ and bound to Python through pybind11, so many of the methods that can be called from Python can also be called from C++. This allows compiled code and Python to share the same data, which is particularly good for adding array-at-a-time Python interfaces to C++ libraries that generate complex objects.

Numba's ability to JIT-compile Python functions is also very useful for analyzing complex structures. A second implementation of Awkward Arrays as a Numba extension allows them to be used in JIT-compiled Python.

(At the time of the conference, a GPU backend will be in development, but I may be able to show preliminary results.)

### Conclusions

Although most data analysis tools target rectilinear data, there's nothing domain-specific about nested, variable-length, JSON-like data. I want to present Awkward Array to the wider community to see what other data analysts might do with it.

Thank you!

### References

I have given three recent conference presentations on Awkward Array, one with a video.

   * StrangeLoop (computer science audience) on September 14, 2019.
     Video of my presentation: https://youtu.be/2NxWpU7NArk

   * PyHEP (particle physics audience) on October 17, 2019.
     Abstract and slides: https://indico.cern.ch/event/833895/contributions/3577882

   * CHEP (particle physics audience) on November 7, 2019.
     Abstract and slides: https://indico.cern.ch/event/773049/contributions/3473258
     Proceedings (attached below): https://arxiv.org/abs/2001.06307

The old (in use at the time of writing) and new versions of Awkward Array are in two GitHub repos. In the months before SciPy, "awkward-1.0" will move to "awkward-array" and the current "awkward-array" will move to "awkward-0.x", but the "awkward-1.0" redirect will always work.

   * https://github.com/scikit-hep/awkward-array
   * https://github.com/scikit-hep/awkward-1.0

## Keywords

   * NumPy
   * Numba
   * C++
   * Apache Arrow
   * Columnar data
   * AOS-to-SOA
   * Ragged array
   * Jagged array
   * JSON

## Other

**Type of submission:** Talk.

**Specialized track:** High Performance Python (if not General).
