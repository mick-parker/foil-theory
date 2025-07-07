1 Scrapbook Epistemology
Concept Note
We often imagine knowledge as a coherent, unified 'book' - logically ordered, fully integrated. In reality, our minds resemble messy scrapbooks: fragmented, patchy collections of loosely connected pieces. Rather than forming a single narrative, our beliefs, memories, and categories emerge as local constructions pasted together over time. This approach emphasises how humans adaptively incorporate inconsistencies rather than eliminate them, leading to greater flexibility in learning and problem-solving. For philosophers, this challenges traditional notions of rational coherence. Cognitive scientists and developmental psychologists see this reflected in children’s partial, evolving mental models. AI researchers might interpret it as a move away from monolithic symbolic systems toward dynamic, patch-based learning architectures.

Premises:
P1. Knowledge structures are incrementally assembled rather than globally designed.
P2. Contradictory fragments often coexist and inform behaviour.
P3. Flexibility and adaptability are favoured over consistency.

Conclusion:
C1. Understanding minds as scrapbooks highlights human cognitive resilience and suggests a shift away from strict coherence models toward dynamic, modular epistemologies.

Annotation:
Contrast (foil) theory provides a patch-based, non-unified approach to membership.
Conceptual spaces resemble 'scrapbooks' - not continuous smooth prototypes but fragments distinguished by foils.
Evidence: Supporting evidence argues similarity is diffuse, whereas foils create sharper, localised conceptual fragments.

Supporting Evidence:
Summary: Knowledge is fragmentary and contrastively patch-based, rather than smoothly continuous.
Equation: P={p:GFCI(p,F)>τ}P={p:GFCI(p,F)>τ}
Code Snippet: P_mask = Z_gfci > gfci_threshold

import numpy as np

# Scrapbook-style: local patch storage of contrasts
patches = {}

def store_patch(p, f):
    key = tuple(np.round(p, 2))
    patches[key] = {"foil": f, "contrast": np.linalg.norm(p - f)}

# Example point and foil
p = np.array([1.0, 0.5])
f = np.array([0.0, 0.0])

store_patch(p, f)
print(patches)

Heatmap Reference: Left plot (GFCI heatmap), shows discrete ‘patches’ instead of gradient similarity zones.

import numpy as np
import matplotlib.pyplot as plt

F = np.array([[0, 0]])
x = np.linspace(-2, 2, 100)
y = np.linspace(-2, 2, 100)
X, Y = np.meshgrid(x, y)

Z = np.sqrt((X - F[0,0])**2 + (Y - F[0,1])**2)

plt.imshow(Z, extent=(-2, 2, -2, 2), origin='lower', cmap='plasma')
plt.scatter(F[:, 0], F[:, 1], color='red', label='Foil')
plt.colorbar(label='Local Patch "Contrast"')
plt.title("Scrapbook Epistemology: Local Patch Contrast")
plt.legend()
plt.show()

2 Foil Theory
Concept Note
Most theories of concept formation emphasise similarity: we group things based on shared features. Foil Theory proposes that contrast - distinguishing what something is not - is the true cognitive primitive. Instead of first identifying 'dogness' by shared traits, minds first exclude what isn’t a dog (cat, chair, rock). This contrast-based approach simplifies learning, minimises cognitive resources, and better matches how young children and even some animals form categories. Philosophically, it aligns with negative ontologies and contrastive semantics. Cognitive scientists might connect it to discrimination tasks and error-driven learning. In AI, contrastive learning methods already reflect this idea empirically.

Premises:
P1. Minds favour contrastive exclusion over exhaustive similarity search.
P2. Foils (negatives) provide sharper boundaries and cognitive economy.
P3. Developmental evidence supports early contrast-based categorisation.

Conclusion:
C1. Concepts emerge primarily through contrasts with foils, not similarity clusters, reshaping how we understand categorisation and learning.

Annotation:
Contrast (foil) is the primary primitive, not derivative of similarity or prototypes.
Heatmaps show that foils directly define boundaries rather than approximate a centre.
GFCI quantifies this contrast, showing explicit dependence on foils rather than internal coherence.

Supporting Evidence:
Summary: Conceptual membership defined primarily by contrast with foils, not by distance to a prototype.
Equation: GFCI(p,f)=∥p−f∥∥p∥+∥f∥GFCI(p,f)=∥p∥+∥f∥∥p−f∥​ 
Code Snippet: def gfci(p, F): dists = np.linalg.norm(F - p, axis=1), closest_f = F[np.argmin(dists)] return np.linalg.norm(p - closest_f) / (np.linalg.norm(p) + np.linalg.norm(closest_f) + 1e-8)

import numpy as np

F = np.array([[0, 0], [1, 1]])

def contrast(p, F):
    dists = np.linalg.norm(F - p, axis=1)
    return np.min(dists)

p = np.array([2.0, 2.0])
score = contrast(p, F)
print("Contrast score:", score)

Heatmap Reference: Left plot shows contrast-defined set boundary.

import numpy as np
import matplotlib.pyplot as plt

F = np.array([[0, 0], [1, 1]])
x = np.linspace(-2, 3, 100)
y = np.linspace(-2, 3, 100)
X, Y = np.meshgrid(x, y)

Z = np.min([np.sqrt((X - fx)**2 + (Y - fy)**2) for fx, fy in F], axis=0)

plt.imshow(Z, extent=(-2, 3, -2, 3), origin='lower', cmap='viridis')
plt.scatter(F[:, 0], F[:, 1], color='red', label='Foils')
plt.colorbar(label='Contrast Distance')
plt.title("Foil Theory: Minimum Contrast Field")
plt.legend()
plt.show()

3 Boundary Detection in Early Concept Formation as a Parsing Problem 
Concept Note
Before we can categorise, we must parse: break the world into discrete chunks. 'Boundary Detection in Early Concept Formation as Parsing Problem' argues that parsing is the first cognitive act - more fundamental than similarity or contrast. Think of how an infant must segment continuous visual and auditory streams before recognising objects or words. Parsing shapes what counts as an 'entity' at all. This view connects to computational parsing in AI and the perceptual segmentation seen in developmental psychology. Philosophically, it suggests concepts depend on pre-conceptual operations, challenging essentialist or purely representational accounts.

Premises:
P1. Continuous sensory input must be parsed into units before categorisation.
P2. Parsing determines the granularity and identity of perceived objects.
P3. Parsing constraints shape all higher-level conceptualisation.

Conclusion:
C1. Concept formation presupposes parsing, making boundary detection a foundational problem in perception and cognition.

Annotation:
Before categorising or assigning membership, we parse using boundaries.
Foil-based boundaries (GFCI threshold) offer a constructive parsing mechanism in metric space.
Parsing here is based on contrast, not on gradual similarity.

Supporting Evidence:
Summary: Boundaries derived from contrast parsing precede categorisation.
Equation: Parse region: {p:GFCI(p,F)>τ}{p:GFCI(p,F)>τ}
Code Snippet: axs[0].contour(X, Y, P_mask, levels=[0.5], colors='white', linewidths=2, linestyles='--')

import numpy as np

F = np.array([[0, 0], [1, 1]])

def parse_decision(p, F, threshold=1.5):
    min_dist = np.min(np.linalg.norm(F - p, axis=1))
    return min_dist > threshold

p = np.array([2.0, 2.0])
result = parse_decision(p, F)
print("Parsed as separate object?", result)

Heatmap Reference: Left plot, white dashed contour shows parsed set.

import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-2, 2, 100)
y = np.linspace(-2, 2, 100)
X, Y = np.meshgrid(x, y)

Z = np.heaviside(X + Y, 0.5)

plt.imshow(Z, extent=(-2, 2, -2, 2), origin='lower', cmap='Greys')
plt.contour(X, Y, Z, levels=[0.5], colors='blue', linewidths=2)
plt.title("Boundary as Parsing (Diagonal Threshold)")
plt.show()

4 Boundary Detection as a Pre-requisite of Individuation 
Concept Note
Once parsed, we must determine individuation: what counts as a single object or entity. For example, is a flock of birds one thing or many? 'Boundary Detection as a Pre-requisite of Individuation' extends the parsing thesis, arguing that individuation is a second-order act dependent on parsing boundaries. This thesis highlights cultural variation (cognitive anthropology) in how different societies individuate objects and events. In AI, this resembles object tracking and segmentation. For developmental psychology, it explains differences in object permanence and individuation tasks. Philosophically, it challenges assumptions about objective 'individuals' in metaphysics.

Premises:
P1. Parsed segments require decisions about individuation.
P2. Individuation depends on context, function, and observer constraints.
P3. Different systems (cultural, biological, artificial) can individuate differently.

Conclusion:
C1. Individuation emerges as a contingent, system-dependent act following boundary parsing, reframing what counts as an 'individual' or 'object.'

Annotation:
Boundaries from GFCI parsing delineate discrete 'objects' or regions.
Heatmap contours show individuation explicitly: set P is well-separated.
Foil-driven parsing implies individuation precedes any abstract set membership.

Supporting Evidence:
Summary: Parsing by contrast individuates distinct ‘objects’ or set members.
Equation: Boundary formally given by: ∂P=P‾∩X∖P‾∂P=P∩X∖P​ but here replaced by an explicit contrast-driven region.

import numpy as np

F = np.array([[0, 0]])
P = np.array([[2, 2]])

def individuate(p, F, tau=1.0):
    dist = np.linalg.norm(p - F[0])
    return dist > tau

for p in P:
    print("Individuated?", individuate(p, F))

Heatmap Reference: The dashed GFCI contour indicates individuated set P.

import numpy as np
import matplotlib.pyplot as plt

F = np.array([[0, 0]])
x = np.linspace(-2, 2, 100)
y = np.linspace(-2, 2, 100)
X, Y = np.meshgrid(x, y)

dist = np.sqrt((X - F[0,0])**2 + (Y - F[0,1])**2)
mask = dist > 1.0

plt.imshow(mask, extent=(-2, 2, -2, 2), origin='lower', cmap='gray')
plt.scatter(F[:, 0], F[:, 1], color='red', label='Foil')
plt.title("Boundary as Individuation")
plt.legend()
plt.show()

5 FCI Variant Cluster
Concept Note
We often think of categories as groups of similar items - but this overlooks the crucial role of contrast in how we carve up the world. The Foil Contrast Index (FCI) and its variants provide a formal way to measure and model these contrasts. Instead of merely describing what an object is, FCI-based approaches explicitly quantify what it is not, thus highlighting the ‘foil space’ that shapes category boundaries. By weighting differences, geometrically modelling contrast spaces, or probabilistically representing uncertainty, FCI variants allow us to track how sharply or fuzzily a concept is distinguished from alternatives.
For philosophers, this offers a new tool to analyse the problem of universals and natural kinds quantitatively. Cognitive scientists and developmental psychologists can explore how children or agents learn by minimising contrast-based error signals rather than optimising similarity metrics. AI and ML researchers might find it resonates with contrastive learning objectives and anomaly detection frameworks. Cognitive anthropologists can investigate cross-cultural variation in how foil contrasts are emphasised or minimised.

Premises:
P1. Concepts are shaped as much by what they exclude as by what they include.
P2. Quantifying contrasts provides deeper insight into category formation and maintenance.
P3. Weighted, geometric, or probabilistic variants capture different cognitive and cultural emphases.

Conclusion:
C1. The FCI Variant Cluster formalises the central role of contrast in concept formation, offering a powerful quantitative framework to bridge philosophy, cognitive science, AI, and anthropology.

Annotation:
GFCI is a variant of FCI adapted to geometric contexts.
Provides a family of formal contrast metrics for defining membership thresholds systematically.
Supports the thesis that FCI variants create a cluster of definable, empirical measures.

Supporting Evidence:
Summary: GFCI represents one member of a family of formal contrast indices (FCI variants).
Equation: Generalised FCI form: FCI(p,f)=Δ(p,f)N(p,f)FCI(p,f)=N(p,f)Δ(p,f)​ with ΔΔ and NN chosen appropriately (e.g., Euclidean norm in GFCI).
Code Snippet: Same as GFCI function above.

import numpy as np

F = np.array([[0, 0], [1, 1]])

def gfci(p, F):
    dists = np.linalg.norm(F - p, axis=1)
    closest_f = F[np.argmin(dists)]
    return np.linalg.norm(p - closest_f) / (np.linalg.norm(p) + np.linalg.norm(closest_f) + 1e-8)

p = np.array([2.0, 2.0])
score = gfci(p, F)
print("GFCI score:", score)

Heatmap Reference: GFCI heatmap, showing concrete application of a specific variant.

import numpy as np
import matplotlib.pyplot as plt

F = np.array([[0, 0], [1.5, 1.5]])
x = np.linspace(-2, 3, 100)
y = np.linspace(-2, 3, 100)
X, Y = np.meshgrid(x, y)

distances = np.array([np.sqrt((X - fx)**2 + (Y - fy)**2) for fx, fy in F])
Z = np.max(distances, axis=0) / (np.sum(np.abs(F)) + 1e-6)  # simple FCI variant

plt.imshow(Z, extent=(-2, 3, -2, 3), origin='lower', cmap='cividis')
plt.scatter(F[:, 0], F[:, 1], color='red', label='Foils')
plt.colorbar(label='FCI Variant Value')
plt.title("FCI Variant Cluster Field")
plt.legend()
plt.show()

6 The Problem of Universals as the Inverse of the Principle of Individuation 
Concept Note
Traditional metaphysics treats universals as timeless, objective kinds. This thesis suggests that universals emerge from shared parsing and individuation patterns. If many minds parse and individuate the same way, certain patterns become 'universal.' This reframes universals as dynamic, collective stabilisations rather than eternal essences. Philosophers might see this as a new middle ground between realism and nominalism. Cognitive scientists and anthropologists can explore how parsing constraints lead to cross-cultural convergence. In AI, this supports building shared taxonomies grounded in perceptual constraints.

Premises:
P1. Universals imply shared categorisation among observers.
P2. Parsing and individuation are prerequisites for category formation.
P3. Shared constraints yield stable, convergent patterns across agents.

Conclusion:
C1. Universals arise dynamically from shared parsing and individuation constraints, rather than pre-existing as metaphysical absolutes.

Annotation:
Shared contrastive constraints (using finite foils) create universal parsing boundaries across individuals or systems.
The metric space approach suggests these parsing boundaries do not depend on subjective similarity judgments.

Supporting Evidence:
Summary: Contrastive boundaries are data-driven and universalisable across observers.
Equation: P={p:min⁡f∈FGFCI(p,f)>τ}P={p:f∈Fmin​GFCI(p,f)>τ} 

import numpy as np

F = np.array([[0, 0]])
p = np.array([1.0, 1.0])

def universal_boundary(p, F):
    return np.linalg.norm(p - F[0]) > 0.5

print("Universal boundary passed?", universal_boundary(p, F))

Heatmap Reference: Robustness of GFCI-defined boundaries to foil changes.

import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-3, 3, 150)
y = np.linspace(-3, 3, 150)
X, Y = np.meshgrid(x, y)

universal_pattern = np.sin(X) * np.cos(Y)
mask = universal_pattern > 0.5

plt.imshow(universal_pattern, extent=(-3, 3, -3, 3), origin='lower', cmap='Spectral')
plt.contour(X, Y, mask, levels=[0.5], colors='black', linewidths=1.5)
plt.title("Boundary + Universals: Shared Pattern Parsing")
plt.colorbar(label='Universal Pattern Value')
plt.show()

7 Similarity as Cellular Automata 
Concept Note
Could we generate internal 'kinds' without external similarity judgments? Inspired by von Neumann’s self-replicating automata and Conway’s Game of Life, this thesis proposes that cellular automata can model how kinds emerge purely from internal dynamics. Patterns (e.g., gliders, oscillators) act as functional 'kinds' without an external classifier. This formal demonstration addresses Quine’s problem of similarity and natural kinds. For philosophers, it offers a formal alternative to resemblance theories. For AI and cognitive scientists, it models self-organising systems capable of internal classification.

Premises:
P1. Automata generate emergent, stable patterns from simple rules.
P2. Internal dynamics can define functional classes without external similarity metrics.
P3. Self-generated kinds model internal ontologies.

Conclusion:
C1. Cellular automata provide a formal model for defining kinds internally, sidestepping external similarity problems and reshaping natural kind debates.

Annotation (implied):
Emergent pattern separation in cellular automata parallels contrastive parsing.
The explicit constructive contrast models emergent individuation like CA pattern formation.
Heatmap structures echo these emergent patches.

Supporting Evidence:
Summary: Dynamic emergence of discrete patches analogous to automata patterns.
Code/Visual Pointer: GFCI heatmap structure resembles emergent patches.

import numpy as np

grid = np.zeros((5, 5))
grid[2, 2] = 1  # initial "seed"

def evolve(grid):
    new_grid = grid.copy()
    new_grid[1:4, 1:4] += 1  # simplistic local update
    return new_grid

new_grid = evolve(grid)
print(new_grid)

Heatmap Reference: Emergent contour lines reminiscent of automata local attractors.

import numpy as np
import matplotlib.pyplot as plt

grid = np.zeros((10, 10))
grid[5, 5] = 1

for _ in range(3):  # evolve for a few steps
    new_grid = grid.copy()
    new_grid[4:7, 4:7] += 0.5
    grid = new_grid

plt.imshow(grid, cmap='Blues')
plt.title("Cellular Automata: Local Emergence")
plt.colorbar()
plt.show()

8 Concepts as Foils by Parsing 
Concept Note
Combining Foil Theory and parsing, this thesis proposes that concepts emerge as contrasts created by parsing operations, not by grouping similarities. Parsing imposes initial boundaries; contrasts refine these into usable concepts. This hybrid model explains rapid category formation, cross-modal learning, and even cultural variations. Philosophically, it provides a unifying framework that avoids essentialist traps. In AI, it suggests contrastive parsing as a basis for efficient, scalable concept learning.

Premises:
P1. Parsing imposes primitive boundaries on continuous input.
P2. Contrasts clarify and sharpen parsed distinctions into concepts.
P3. Conceptual learning relies more on parsing-contrast interaction than on similarity grouping.

Conclusion:
C1. Concepts arise from contrastive parsing operations, providing a unified, non-essentialist foundation for categorisation.

Annotation:
Combines parsing logic (boundaries first) with explicit contrast metrics (GFCI).
Code illustrates how parsing regions emerge purely from contrast.
Shows that parsing and contrast are not separable but jointly implemented.

Supporting Evidence:
Summary: Parsing and contrast are implemented together via GFCI thresholding.
Equation: {p:GFCI(p,F)>τ}{p:GFCI(p,F)>τ} 
Code Snippet: P_mask = Z_gfci > gfci_threshold

import numpy as np

F = np.array([[0, 0]])
p = np.array([1.5, 1.5])

def contrastive_parse(p, F, tau=1.0):
    return np.linalg.norm(p - F[0]) > tau

print("Contrastive parse valid?", contrastive_parse(p, F))

Heatmap Reference: Left plot shows how parsing and contrast define same region.

import numpy as np
import matplotlib.pyplot as plt

F = np.array([[0, 0]])
x = np.linspace(-3, 3, 100)
y = np.linspace(-3, 3, 100)
X, Y = np.meshgrid(x, y)

dist = np.sqrt((X - F[0,0])**2 + (Y - F[0,1])**2)
mask = (dist > 1) & (dist < 2)

plt.imshow(dist, extent=(-3, 3, -3, 3), origin='lower', cmap='cool')
plt.contour(X, Y, mask, levels=[0.5], colors='white', linewidths=2, linestyles='--')
plt.scatter(F[:, 0], F[:, 1], color='yellow', label='Foil')
plt.title("Contrastive Parsing Region")
plt.legend()
plt.show()

9 Dynamic Scrapbook Epistemology 
Concept Note
Building on Scrapbook Epistemology and automata modelling, this thesis describes knowledge systems as dynamic scrapbooks: evolving collections of partial, constantly updated pattern libraries. Instead of a fixed hierarchy or single logic, minds (or AI systems) adaptively patch and prune fragments based on new inputs. This approach reflects real cognitive plasticity, cultural fluidity, and supports lifelong learning in AI. Philosophically, it aligns with anti-foundationalism and pluralism.

Premises:
P1. Minds accumulate fragmented, partial knowledge pieces.
P2. These fragments are dynamically updated and restructured.
P3. Automata models can simulate evolving, patch-based knowledge systems.

Conclusion:
C1. Knowledge functions as a dynamic scrapbook: a flexible, evolving assembly of partial, pattern-based fragments rather than a coherent fixed system.

Annotation:
Movement or change of foils would dynamically reshape conceptual regions.
'Scrapbook' patches evolve as foils move - directly modelled through dynamic GFCI boundaries.

Supporting Evidence:
Summary: Moving foils dynamically updates patch regions.
Visual Pointer: Suggested animation direction.
Code Snippet (conceptual): F = np.array([[-2, -1], [2 + delta_x, 1.5 + delta_y]])

scrapbook = []

def add_patch(patch):
    scrapbook.append(patch)

# New observation patch
patch = {"point": [1.0, 0.5], "contrast": 1.2}
add_patch(patch)
print(scrapbook)

Heatmap Reference: Implied dynamic recomputation of GFCI heatmap.

import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-5, 5, 150)
y = np.linspace(-5, 5, 150)
X, Y = np.meshgrid(x, y)

# Simulate "scrapbook" patches - dynamic evolving regions
patch1 = np.exp(-((X+2)**2 + (Y+2)**2))
patch2 = np.exp(-((X-2)**2 + (Y-1)**2))
patch3 = np.exp(-((X)**2 + (Y-3)**2))

combined = patch1 + patch2 + 0.5 * patch3
threshold_mask = combined > 0.3

plt.imshow(combined, extent=(-5, 5, -5, 5), origin='lower', cmap='plasma')
plt.contour(X, Y, threshold_mask, levels=[0.5], colors='white', linewidths=1.5)
plt.title("Dynamic Scrapbook: Evolving Patch Regions")
plt.colorbar(label='Patch Intensity')
plt.show()

10 Universals by Parsing
Concept Note
Extending the Boundary Detection and Universals thesis, this view argues that universals only arise where parsing constraints are shared and stable. 'Parsing-First Universals' emphasises that universals are not only culturally emergent but require deeply ingrained perceptual and cognitive constraints. This links metaphysics, cognitive science, and developmental psychology directly. AI researchers might explore it in multi-agent systems developing shared taxonomies. Philosophers see it as a new nominalism-realism hybrid.

Premises:
P1. Universals imply cross-observer consistency.
P2. Parsing is necessary to impose comparable structures.
P3. Only stable, shared parsing operations yield possible universals.

Conclusion:
C1. Universals are emergent consequences of shared parsing constraints, challenging static or essentialist views of general categories.

Annotation:
Parsing via boundaries is a universal precursor to categorisation.
GFCI as a metric-based parsing mechanism supports emergence of parse-stable universals regardless of prototypes.

Supporting Evidence:
Summary: Universals emerge from stable parsing boundaries across contexts.
Equation: Stability of {p:GFCI(p,F)>τ}{p:GFCI(p,F)>τ} across variations in F.

import numpy as np

def parse_first(p, threshold=1.0):
    return np.linalg.norm(p) > threshold

p = np.array([1.2, 1.2])
print("Universal parsing result:", parse_first(p))

Heatmap Reference: Left plot as a snapshot of universal parse boundary.

import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-4, 4, 150)
y = np.linspace(-4, 4, 150)
X, Y = np.meshgrid(x, y)

pattern = np.heaviside(np.sin(X) + np.cos(Y), 0.5)

plt.imshow(pattern, extent=(-4, 4, -4, 4), origin='lower', cmap='magma')
plt.contour(X, Y, pattern, levels=[0.5], colors='lime', linewidths=1.5)
plt.title("Parsing-First Universals")
plt.show()

11 Formalising Foils 
Concept Note
Beyond static contrasts, minds simulate counterfactual alternatives - 'what did not happen' - to refine concepts and explanations. This thesis proposes that conceptual foils can be formalised as generative simulations, aligning with counterfactual reasoning (e.g., in causal models). In AI, it connects to contrastive learning and adversarial example generation. For cognitive scientists, it illuminates how mental simulations structure learning and explanation.

Premises:
P1. Conceptual contrasts often involve imagining absent possibilities.
P2. Simulation underlies human prediction, explanation, and learning.
P3. Counterfactual contrasts help define conceptual boundaries.

Conclusion:
C1. Conceptual contrasts can be operationalised as simulations of alternative scenarios, deepening our understanding of reasoning and conceptual refinement.

Annotation:
Heatmaps provide direct simulation of alternative contrastive definitions by adjusting foils.
Possibility to simulate alternative 'worldviews' or membership by moving foils.

Supporting Evidence:
Summary: Simulating alternative concepts by modifying foils.
Code Snippet (conceptual): F = np.array([[-3, 0], [3, 0]])  # new foil configuration

import numpy as np

F = np.array([[0, 0], [1, 1]])
p_variants = [np.array([2.0, 2.0]), np.array([0.5, 0.5])]

def simulate_contrast(p, F):
    return np.min(np.linalg.norm(F - p, axis=1))

for p in p_variants:
    print("Simulated contrast score:", simulate_contrast(p, F))

Heatmap Reference: Future direction proposed in Part III to simulate conceptual contrast shifts.

import numpy as np
import matplotlib.pyplot as plt

F = np.array([[0, 0], [1, 1]])
x = np.linspace(-2, 3, 100)
y = np.linspace(-2, 3, 100)
X, Y = np.meshgrid(x, y)

Z = np.min([np.sqrt((X - fx)**2 + (Y - fy)**2) for fx, fy in F], axis=0)

plt.imshow(Z, extent=(-2, 3, -2, 3), origin='lower', cmap='magma')
plt.scatter(F[:, 0], F[:, 1], color='cyan', label='Foils')
plt.colorbar(label='Simulated Contrast')
plt.title("Contrastive Simulation")
plt.legend()
plt.show()

12 Conceptual Economy 
Concept Note
All ontological and conceptual structures, this thesis argues, reflect a principle of economy: minimal parsing, minimal contrasts, and minimal cognitive cost. Rather than maximising feature representation, systems prioritise simplicity and efficiency. This explains why categories are often fuzzy and why exceptions are tolerated. It aligns with cognitive minimalism, Ockham’s Razor, and satisfying [?satisficing (e.g., optimisation)]. For AI, it suggests optimisation principles beyond accuracy alone. Philosophically, it offers a unifying meta-principle for conceptual engineering.

Premises:
P1. Cognitive and ontological structures are resource-constrained.
P2. Systems favour simpler, more efficient categorisation over exhaustive accuracy.
P3. Fuzzy and approximate categories reflect economy.

Conclusion:
C1. Concepts and kinds emerge from a principle of metaphysical economy, prioritising minimal parsing and contrast rather than maximal descriptive precision.

Annotation:
Economises conceptual structure: defines categories only where contrastive parsing is necessary.
No infinite neighbourhoods or closures (topological overhead), only finite foils.

Supporting Evidence:
Summary: Avoids unnecessary topological constructions; uses finite, constructive foils.
Equation: Only finite F needed; no closure operator.

import numpy as np

points = [np.array([1, 1]), np.array([2, 2])]
F = np.array([[0, 0]])

def economical_score(p, F):
    return np.linalg.norm(p - F[0])

for p in points:
    print("Economical contrast score:", economical_score(p, F))

Heatmap Reference: GFCI-defined regions avoid blurry topological ‘fuzz.’

import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-3, 3, 100)
y = np.linspace(-3, 3, 100)
X, Y = np.meshgrid(x, y)

Z = np.sqrt(X**2 + Y**2)
mask = Z < 1.5

plt.imshow(Z, extent=(-3, 3, -3, 3), origin='lower', cmap='viridis')
plt.contour(X, Y, mask, levels=[0.5], colors='white', linewidths=2)
plt.title("Metaphysical Economy: Minimal Regions")
plt.colorbar(label='Radial Distance')
plt.show()

13 Concept Formation by Parsing and Foils 
Concept Note
This integrative thesis proposes that concepts, kinds, and universals arise from parsing and contrast processes rather than similarity or essence. Parsing breaks up experience, contrasts sharpen distinctions, and shared constraints stabilise universals. Cellular automata and dynamic scrapbooks formally model these dynamics. This unified framework reframes debates in metaphysics, epistemology, cognitive science, AI, and anthropology. It offers a powerful alternative to traditional essentialist or purely resemblance-based accounts.

Premises:
P1. Parsing and contrast precede similarity in shaping concepts.
P2. Dynamic systems can model emergent kinds internally.
P3. Shared parsing explains universals without metaphysical essences.

Conclusion:
C1. A contrastive parsing framework unifies concept formation, categorisation, and universals, offering a dynamic, emergent alternative to static metaphysical theories.

Annotation:
Unified synthesis: parsing first, contrast as primitive, formal empirical support (heatmaps).
Demonstrates full contrastive, patch-based epistemology with empirical, geometric, and formal justification.

Supporting Evidence:
Summary: Integration of contrast as primitive, parsing-first logic, and empirical support.
Visual Pointer: Heatmaps - left plot (GFCI) vs right plot (similarity).
Key Code Snippet: fig, axs = plt.subplots(1, 2, figsize=(14, 6))

import numpy as np

F = np.array([[0, 0]])
p = np.array([1.5, 1.5])

def meta_contrast(p, F):
    dist = np.linalg.norm(p - F[0])
    parse_ok = dist > 1.0
    return parse_ok, dist

parse_ok, score = meta_contrast(p, F)
print("Meta parse?", parse_ok, "| Contrast score:", score)

Heatmap Reference: Final combined plots demonstrating the full unification visually.

import numpy as np
import matplotlib.pyplot as plt

F = np.array([[0, 0]])
x = np.linspace(-3, 3, 100)
y = np.linspace(-3, 3, 100)
X, Y = np.meshgrid(x, y)

dist = np.sqrt((X - F[0,0])**2 + (Y - F[0,1])**2)
mask = dist > 1.5

plt.imshow(dist, extent=(-3, 3, -3, 3), origin='lower', cmap='inferno')
plt.contour(X, Y, mask, levels=[0.5], colors='white', linewidths=2, linestyles='--')
plt.scatter(F[:, 0], F[:, 1], color='lime', label='Foil')
plt.colorbar(label='Contrast Distance')
plt.title("Meta-Thesis: Parsing + Contrast Field")
plt.legend()
plt.show()
